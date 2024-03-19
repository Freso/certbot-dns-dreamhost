# certbot-dns-dreamhost
[Certbot](https://certbot.eff.org/) plugin to authenticate DreamHost domains

This plugin is [published on pypi](https://pypi.org/project/certbot-dns-dreamhost/).

## Installation

### Via `pip`

In order to use a `pip` installed plugin on certbot, you also have to install certbot via `pip`. See the [instructions on installing Certbot via `pip` on Certbot's website](https://certbot.eff.org/instructions?ws=other&os=pip).

To install this plugin you can use `sudo /opt/certbot/bin/pip install certbot-dns-dreamhost`.

## Usage

`certbot-dns-dreamhost` needs a credentials file to access the DreamHost API. Make sure this file can only be accessed by root, since anyone with these credentials may delete all your DNS records.

1. Get your API key from DreamHost with permission for `dns-*`. You can get it on the [Web Panel API page](https://panel.dreamhost.com/?tree=home.api).

2. Create your credentials file: `/etc/letsencrypt/dns-dreamhost.ini` and enter your API key and the base URL for DreamHost's API (usually `https://api.dreamhost.com/`), as below (keep the variables names):
```ini
dns_dreamhost_baseurl = "<api_base_url>"
dns_dreamhost_api_key = "<api_key>"
```

3. You can secure your file and assure that only your user is able to read and write on it: 
```bash
chmod 0600 /etc/letsencrypt/dns-dreamhost.ini
```

4. Try to issue a certificate:
```bash
certbot certonly --authenticator dns-dreamhost \
--dns-dreamhost-credentials /etc/letsencrypt/dns-dreamhost.ini \
-d '*.example.com'
```

5. Congrats!
