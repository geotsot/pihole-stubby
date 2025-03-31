# Install & Setup Stubby with Pi-hole for NextDNS

## What is Stubby?

[Stubby](https://github.com/getdnsapi/stubby) is an application that acts as a local DNS Privacy stub resolver (using [DNS-Over-TLS](https://datatracker.ietf.org/doc/html/rfc7858)). Stubby encrypts DNS queries sent from a client machine (desktop or laptop) to a DNS Privacy resolver increasing end user privacy.

## Installing Stubby

Ensure the "Universe" repository is enabled and ensure the repositories are up to date:

```bash
sudo add-apt-repository universe && sudo apt update
```

Install Stubby:

```bash
sudo apt install stubby -y
```

## Configure `stubby`

Back up and replace the default `stubby.yml` file with the stubby.yml file in this repo:

```bash
sudo mv /etc/stubby/stubby.yml /etc/stubby/stubby.backup.yml && sudo wget -O /etc/stubby/stubby.yml https://raw.githubusercontent.com/geotsot/pihole-stubby/main/stubby.yml
```

You can edit and uncomment the configuration file to change the DNS servers used. **(Default: NextDNS)**

If you are creating a custom configuration file you can find more info below:

[DNS Privacy](https://dnsprivacy.org/dns_privacy_daemon_-_stubby/configuring_stubby/)

## Restart Stubby to recognize the new configuration

```bash
sudo systemctl restart stubby && sudo systemctl status stubby
```

## Configure Pi-hole

Configure Pi-hole to use unbound as your recursive DNS server and untick any other upstream DNS Server:

### Settings -> DNS -> Custom DNS Servers**

```bash
127.0.0.1#5300
```

Click save.

![screenshot at 2025-03-31](https://imgur.com/y2bxIwN)
