# device-openarc
Provides an OpenARC appliance.

This appliance does the following:

- Automatically configures OpenARC's configuration files before startup.
- Binds securely to the unix domain socket /run/openarc/openarc.sock.
- Enables verification of email.
- Optionally adds a domain, selector and key to the configuration, to enable signing.
- Autostarts on server restart.

## before

- Deploy the device-openarc package.

```
[root@server ~]# dnf install device-openarc
```

- Deploy optional RSA key needed to /etc/pki/tls/private, root only.

```
[root@server ~]# ls -l /etc/pki/tls/private/
total 12
-rw-------. 1 root root  887 Oct  4 11:45 example-dkim.pem
```

## set domain

To set a domain, do the following:

```
[root@server ~]# device services mail smtp arc set domain=example.com selector=default key=example-dkim
```

## enable

To switch the appliance on, run this.

```
[root@server ~]# device services mail smtp arc enable 
```

## disable

To switch the appliance off, run this.

```
[root@server ~]# device services mail smtp arc disable  
```

## show dns TXT record

To see the resulting DNS TXT record, run this.

```
[root@server ~]# device services mail smtp arc show-dns 
default._domainkey.example.com. 86400 IN TXT "v=DKIM1; p=MIGfMA0G[snip]"
```

