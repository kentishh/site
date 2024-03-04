---
title: "PiBound - a simple script which configures PiHole and Unbound to be your network's recursive DNS server."
date: 2020-10-09T13:26:43Z
draft: false
---

[PiBound](https://github.com/kentishh/pi-bound) is a project built out of love for PiHole and privacy. I wanted to make it as simple as possible to install PiHole and make use of Unbound to be your network's recursive DNS server. Moving away from using your ISP's, Google's or Cloudflare's DNS service is a great way to reduce the amount of eyes that can potentially monitor your internet usage and browsing habits. When we use Unbound as our DNS server, you eliminate the upstream DNS service, becoming your own DNS provider.


## What is PiHole? 

[PiHole](https://pi-hole.net) is an open source network DNS sink-hole, blocking any blacklisted domains before they reach your device. This is especially effective when running on a slower broadband connection, preventing any requests out to known tracking, advertisement or malicious sites can help preserve bandwidth noticeably. I've found over the years that pairing PiHole with a browser extension such as [uBlock origin](https://github.com/gorhill/uBlock) is a great combination that will pretty much block any annoyances when browsing the web. With this configuration, you get the benefits of blocking domains before they even hit your network and any that do get past PiHole will typically be picked up by uBlock and blocked.

## What is Unbound?

[Unbound](https://nlnetlabs.nl/projects/unbound/about/) is a validating, caching, recursive DNS server. It's lightweight enough to run on a Pi-Zero, which is perfect for a project like this. We'll be utilising Unbound to do our DNS recursion as well as it's caching abilities, which will store a local cache of DNS records which can be served to the client immediately. To learn a little bit more about DNS, [take a look at this fun comic](https://howdns.works). 

## How does the script work?

Initially you will be prompted for the installation type you want to continue with, a lot of people that have used this script already have PiHole installed, so I added the functionality to just install Unbound and complete all necessary configuration. 

* Firstly, the script will install PiHole, using the automated installation script method provided by the PiHole developers.
* Secondly, Unbound will be installed, root hints will be downloaded and the required Unbound configuration file will be pulled from the project's GitHub repository. PiHole will be configured to use Unbound as our DNS server.
* Finally, a few DNS checks will take place to ensure DNSSEC is configured and Unbound is working as expected.

### Comparing our own DNS server's performance to public resolvers.

In my testing, I've found for the most part that using my own DNS server has surprisingly been just as fast as using a public resolver such as Google (8.8.8.8), or Cloudflare (1.1.1.1).

See the dig output below when querying *google.com* from Google's DNS servers:

```
$ dig google.com @8.8.8.8 | grep "Query"
;; Query time: 10 msec
```

Compare this to querying *google.com* using my PiBound server: 

```
$ dig google.com @192.168.1.110 | grep "Query"
;; Query time: 2 msec
```

We can assume some caching is happening here on my DNS server. Let's try to query a site outside of my cache:

```
dig networkchuck.coffee @192.168.1.110 | grep "Query"
;; Query time: 182 msec
```

Comparing this to Google's DNS:

```
dig networkchuck.coffee @8.8.8.8 | grep "Query"
;; Query time: 142 msec
```

These query time differences are negligable and will not have a noticeable impact on general performance.