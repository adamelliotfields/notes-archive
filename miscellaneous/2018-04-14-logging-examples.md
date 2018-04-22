# Logging Examples
> :calendar: _April 14, 2018_

Example logging output from Java Spark, Express, and Ghost.

### Spark

```
[Thread-0] INFO org.eclipse.jetty.util.log - Logging initialized @343ms to org.eclipse.jetty.util.log.Slf4jLog
[Thread-0] INFO spark.embeddedserver.jetty.EmbeddedJettyServer - == Spark has ignited ...
[Thread-0] INFO spark.embeddedserver.jetty.EmbeddedJettyServer - >> Listening on 0.0.0.0:4567
[Thread-0] INFO org.eclipse.jetty.server.Server - jetty-9.4.8.v20171121, build timestamp: 2017-11-21T16:27:37-05:00, git hash: 82b8fb23f757335bb3329d540ce37a2a2615f0a8
[Thread-0] INFO org.eclipse.jetty.server.session - DefaultSessionIdManager workerName=node0
[Thread-0] INFO org.eclipse.jetty.server.session - No SessionScavenger set, using defaults
[Thread-0] INFO org.eclipse.jetty.server.session - Scavenging every 660000ms
[Thread-0] INFO org.eclipse.jetty.server.AbstractConnector - Started ServerConnector@41f2b1af{HTTP/1.1,[http/1.1]}{0.0.0.0:4567}
[Thread-0] INFO org.eclipse.jetty.server.Server - Started @526ms
[qtp619564843-12] INFO App - GET /
```

### Express (Morgan Dev)

```
GET / 200 2.774 ms - 25
```

### Express (Morgan Combined)

```
127.0.0.1 - - [14/Apr/2018:16:16:13 +0000] "GET / HTTP/1.1" 200 - "-" "Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0"
```

### Express (Morgan Combined JSON)

```javascript
const logger = morgan((tokens, request, response) => {
  const remote_addr = tokens['remote-addr'](req) || '';
  const remote_user = tokens['remote-user'](req) || '';
  const date = tokens['date'](req, res, 'clf') || '';
  const method = tokens['method'](req) || '';
  const url = tokens['url'](req) || '';
  const http_version = tokens['http-version'](req) || '';
  const status = tokens['status'](req, res) || '';
  const content_length = tokens['res'](req, res, 'content-length') || '';
  const referrer = tokens['referrer'](req) || '';
  const user_agent = tokens['user-agent'](req) || '';

  return JSON.stringify(
    {
      remote_addr,
      remote_user,
      date,
      method,
      url,
      http_version,
      status,
      content_length,
      referrer,
      user_agent
    }, null, 2);
  });

app.use(logger);
```

```json
{
  "remote_addr": "127.0.0.1",
  "remote_user": "",
  "date": "14/Apr/2018:16:50:00 +0000",
  "method": "GET",
  "url": "/",
  "http_version": "1.1",
  "status": "200",
  "content_length": "",
  "referrer": "",
  "user_agent": "Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0"
}
```

### Ghost

```
[2018-04-14 17:22:32] WARN Theme's file locales/en.json not found.
[2018-04-14 17:22:32] INFO Ghost is running in development...
[2018-04-14 17:22:32] INFO Listening on: 127.0.0.1:2368
[2018-04-14 17:22:32] INFO Url configured as: http://localhost:2368/
[2018-04-14 17:22:32] INFO Ctrl+C to shut down
[2018-04-14 17:22:48] INFO "GET /" 200 462ms
[2018-04-14 17:24:34] WARN Ghost has shut down
[2018-04-14 17:24:34] WARN Ghost was running for 2 minutes
```
