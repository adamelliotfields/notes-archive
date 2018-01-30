# Vultr DNS Setup with Google Domains
> :calendar: *January 29, 2018*

Vultr has its own DNS, so you can configure your resource records, Reverse DNS, and DNSSEC all
within the Vultr control panel, and point your Google Domain name to the Vultr name server.

This assumes you've already purchased a domain on Google Domains.

### Add Domain to Vultr

Click the "DNS" tab and then click "Add Domain". Enter your domain name.

### Add Resource Records

Click on the newly added domain name to go to the "Manage DNS Domain" page.

Fill in the data using your own domain name and IP addresses. If you plan on setting up a mail
server, add a MX entry as well.

You can set time-to-live (TTL) to longer if you'd like.

| Type  | Name | Data                 | TTL |
|-------|------|----------------------|-----|
| A     |      | `ipv4_address`       | 300 |
| AAAA  |      | `ipv6_address`       | 300 |
| CNAME | www  | adamelliotfields.com | 300 |
| NS    |      | ns1.vultr.com        | 300 |
| NS    |      | ns2.vultr.com        | 300 |

### Set Reverse DNS

This is the data returned to a reverse DNS lookup (if somebody looks up your IP).

Click on your server, then click "Settings".

Under "Public Network", click on the existing Reverse DNS entry, and set it to your domain.

Do the same for IPv6 as well.

### Configure Google Domains Name Servers

In Google Domains, click "DNS" next to your domain name.

Under "Name Servers", click "Use custom name servers".

Add `ns1.vultr.com` and `ns2.vultr.com`.

### Configure DNSSEC

Back in the Vultr control panel, go to the "Manage DNS Domain" page.

Click on "Zone Settings" and enable DNSSEC Settings.

Take note of the DS Records entries.

Go back to the Google Domains DNS settings. Under DNSSEC, add the corresponding Vultr data:
  - Key Tag: Vultr Key Type
  - Algorithm: Vultr Algorithm
  - Digest Type: Vultr Digest Type
  - Digest: Vultr Digest

It can take a few hours for the changes to propogate. Once everything is live, you can verify your
DNSSEC settings with <http://dnsviz.net>.

You can check your DNS and Reverse DNS lookups with <https://mxtoolbox.com>.
