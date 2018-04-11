# Ghost Nginx Notes
> :calendar: *April 10, 2018*

When installing Ghost using the Ghost CLI tool, it auto configures Nginx and obtains a SSL
certificate using Let's Encrypt.

I wanted to document the configuration settings to use as a reference for future projects.

**References:**
  - <http://nginx.org/en/docs/beginners_guide.html>
  - <https://github.com/h5bp/server-configs-nginx>
  - <https://linode.com/docs/web-servers/nginx/how-to-configure-nginx>
  - <https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-with-http-2-support-on-ubuntu-16-04>
  - <https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04>

### `nginx.conf`

The main Nginx configuration file is `nginx.conf`, located in `/etc/nginx`. This is the entrypoint,
and all additional configuration can be included in here.

The config is structured by blocks and directives. `http {}` is a block, `sendfile on` is a
directive.

```nginx
user www-data;
worker_processes auto;
pid /run/nginx.pid;

events {
    worker_connections 768;
}

http {
    # Basic Settings

    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;
    default_type application/octet-stream;

    include /etc/nginx/mime.types;

    # SSL Settings

    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;

    # Logging Settings

    access_log /var/log/nginx/access.log;
    error_log /var/log/nginx/error.log;

    # Gzip Settings

    gzip on;
    gzip_disable "msie6";

    # Virtual Host Configs

    include /etc/nginx/conf.d/*.conf;
    include /etc/nginx/sites-enabled/*;
}
```

### `mime.types`

The first included file is `mime.types`. This is a long file that maps file extensions to MIME
(Multipurpose Internet Mail Extension) types.

You can read more about it in the Nginx [docs](http://nginx.org/en/docs/http/ngx_http_core_module.html#types).

```nginx
types {
    text/html                                                                  html htm shtml;
    text/css                                                                   css;
    text/xml                                                                   xml;
    image/gif                                                                  gif;
    image/jpeg                                                                 jpeg jpg;
    application/javascript                                                     js;
    application/atom+xml                                                       atom;
    application/rss+xml                                                        rss;

    text/mathml                                                                mml;
    text/plain                                                                 txt;
    text/vnd.sun.j2me.app-descriptor                                           jad;
    text/vnd.wap.wml                                                           wml;
    text/x-component                                                           htc;

    image/png                                                                  png;
    image/tiff                                                                 tif tiff;
    image/vnd.wap.wbmp                                                         wbmp;
    image/x-icon                                                               ico;
    image/x-jng                                                                jng;
    image/x-ms-bmp                                                             bmp;
    image/svg+xml                                                              svg svgz;
    image/webp                                                                 webp;

    application/font-woff                                                      woff;
    application/java-archive                                                   jar war ear;
    application/json                                                           json;
    application/mac-binhex40                                                   hqx;
    application/msword                                                         doc;
    application/pdf                                                            pdf;
    application/postscript                                                     ps eps ai;
    application/rtf                                                            rtf;
    application/vnd.apple.mpegurl                                              m3u8;
    application/vnd.ms-excel                                                   xls;
    application/vnd.ms-fontobject                                              eot;
    application/vnd.ms-powerpoint                                              ppt;
    application/vnd.wap.wmlc                                                   wmlc;
    application/vnd.google-earth.kml+xml                                       kml;
    application/vnd.google-earth.kmz                                           kmz;
    application/x-7z-compressed                                                7z;
    application/x-cocoa                                                        cco;
    application/x-java-archive-diff                                            jardiff;
    application/x-java-jnlp-file                                               jnlp;
    application/x-makeself                                                     run;
    application/x-perl                                                         pl pm;
    application/x-pilot                                                        prc pdb;
    application/x-rar-compressed                                               rar;
    application/x-redhat-package-manager                                       rpm;
    application/x-sea                                                          sea;
    application/x-shockwave-flash                                              swf;
    application/x-stuffit                                                      sit;
    application/x-tcl                                                          tcl tk;
    application/x-x509-ca-cert                                                 der pem crt;
    application/x-xpinstall                                                    xpi;
    application/xhtml+xml                                                      xhtml;
    application/xspf+xml                                                       xspf;
    application/zip                                                            zip;

    application/octet-stream                                                   bin exe dll;
    application/octet-stream                                                   deb;
    application/octet-stream                                                   dmg;
    application/octet-stream                                                   iso img;
    application/octet-stream                                                   msi msp msm;

    application/vnd.openxmlformats-officedocument.wordprocessingml.document    docx;
    application/vnd.openxmlformats-officedocument.spreadsheetml.sheet          xlsx;
    application/vnd.openxmlformats-officedocument.presentationml.presentation  pptx;

    audio/midi                                                                 mid midi kar;
    audio/mpeg                                                                 mp3;
    audio/ogg                                                                  ogg;
    audio/x-m4a                                                                m4a;
    audio/x-realaudio                                                          ra;

    video/3gpp                                                                 3gpp 3gp;
    video/mp2t                                                                 ts;
    video/mp4                                                                  mp4;
    video/mpeg                                                                 mpeg mpg;
    video/quicktime                                                            mov;
    video/webm                                                                 webm;
    video/x-flv                                                                flv;
    video/x-m4v                                                                m4v;
    video/x-mng                                                                mng;
    video/x-ms-asf                                                             asx asf;
    video/x-ms-wmv                                                             wmv;
    video/x-msvideo                                                            avi;
}
```

### `sites-available`

The server configuration files are kept in the `/etc/nginx/sites-available` folder.

Ghost creates 2 files: one for HTTP (port 80), and one for HTTPS (port 443). They are similar except
the HTTPS file includes the SSL certificate locations and additional SSL parameters. HTTPS traffic
is also served over HTTP/2.

Note that there is no `return 301` directive in the HTTP `server` block. This is because Ghost
handles this on its own, based on the URL in your `config.production.json`.

The `server_name` directive is the domain name used to serve requests. The path in the `location`
block is appended to the `server_name`. For example, if the URL is `http://adamelliotfields.com/`,
the directives in the `location /` block will be executed.

The `root` directive is the location on the file system to serve files from. This is used for Let's
Encrypt _webroot_ validation. 

The `/.well-known` path is used for Let's Encrypt challenge validation. Note the use of the tilde
(`~`). This means the path is matched using case-sensitive regular expression matching. Nginx uses
Perl Compatible Regular Expressions (PCRE).

`client_max_body_size` is the maximum file size that can be uploaded via a POST request.

**`adamelliotfields.com.conf`**

```nginx
server {
    listen 80;
    listen [::]:80;

    server_name adamelliotfields.com;
    root /var/www/ghost/system/nginx-root;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:2368;

    }

    location ~ /.well-known {
        allow all;
    }

    client_max_body_size 50m;
}
```

The SSL certificates are generated using [Acme.sh](https://github.com/Neilpang/acme.sh).

The shell command looks like this:

```bash
/etc/letsencrypt/acme.sh \
--issue \
--home /etc/letsencrypt \
--domain adamelliotfields.com \
--webroot /var/www/ghost/system/nginx-root \
--reloadcmd "nginx -s reload" \
--accountemail adam@email.com
```

**`adamelliotfields.com-ssl.conf`**

```nginx
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;

    server_name adamelliotfields.com;
    root /var/www/ghost/system/nginx-root;

    ssl_certificate /etc/letsencrypt/adamelliotfields.com/fullchain.cer;
    ssl_certificate_key /etc/letsencrypt/adamelliotfields.com/adamelliotfields.com.key;
    include /etc/nginx/snippets/ssl-params.conf;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header Host $http_host;
        proxy_pass http://127.0.0.1:2368;

    }

    location ~ /.well-known {
        allow all;
    }

    client_max_body_size 50m;
}
```

The SSL params are included in the HTTPS config. The `ssl_dhparam` directive is the location of the
encryption key generated from running `openssl dhparam -out /etc/nginx/snippets/dhparam.pem 2048`.

The default key has a length of 1024 bits, and it is recommended to generate a stronger key using
2048 (or even 4096) bits.

**`ssl-params.conf`**

```nginx
ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
ssl_prefer_server_ciphers on;
ssl_ciphers 'ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS';
ssl_ecdh_curve secp384r1;
ssl_session_cache shared:SSL:10m;
ssl_session_tickets off;
ssl_stapling on;
ssl_stapling_verify on;

resolver 8.8.8.8 8.8.4.4 valid=300s;
resolver_timeout 5s;

add_header Strict-Transport-Security 'max-age=63072000; includeSubDomains; preload';
add_header X-Frame-Options SAMEORIGIN;
add_header X-Content-Type-Options nosniff;

ssl_dhparam /etc/nginx/snippets/dhparam.pem;
```

### `sites-enabled`

A common convention is to symlink the server configuration files in `sites-available` to
`sites-enabled`. This allows you to only have to edit one file, and the changes will be reflected
through the symlink. If you want to remove a configuration, you can simply delete the symlink,
leaving the actual file in `sites-available` should you want to add it again in the future.
