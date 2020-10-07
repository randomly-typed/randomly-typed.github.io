---
layout: "post_1"
title:  "29 - Great Cannon of China"
date:   2020-10-06
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/29---Great-Cannon-of-China-ekn17j
description: "Lance and JS discuss censoring attacks from China targeting Github."
permalink: /29.html
---

**<a href="https://en.wikipedia.org/wiki/Censorship_of_GitHub#DDoS_attack">Wikipedia</a>**

- At the end of March 2015, China attacked Github with a massive DDoS attack that intermittently crashed the website for multiple days. They were targeting 2 projects, GreatFire and cn-nytimes.
- Over the years China attacked Github multiple times. Blocked traffic with DNS hijacking to Mitm TLS attacks. This is scary considering that China has some trusted Root CA in all of our computers.

**<a href="https://arstechnica.com/information-technology/2015/04/ddos-attacks-that-crippled-github-linked-to-great-firewall-of-china/">Arstechnica 1</a>**

- The JavaScript was silently injected into the traffic of sites that use an analytics service that China-based search engine Baidu makes available so website operators can track visitor statistics.
- load two GitHub pages, one a mirror of anti-censorship site GreatFire.org the other a copy of the China edition of The New York Times.
- Now, Rob Graham, CEO of Errata Security, has traced the origin of the malicious code to China Unicom, the same telecom that has been caught before aiding the massive censorship apparatus known as the Great Firewall of China.

**<a href="https://arstechnica.com/information-technology/2015/03/github-battles-largest-ddos-in-sites-history-targeted-at-anti-censorship-tools/">Arstechnica 2</a>**

Says that the infected Javascript was directly injected when visiting the Baidu search engine.

**<a href="https://citizenlab.ca/2015/04/chinas-great-cannon/">Citizenlab</a>**

- Some people are calling this DDoS tool the Great Canon of China.
- As we mentioned earlier, what’s interesting is that it hijacks traffic from a really large number of computers in China which are not really compromised, other than that they are in China.
- The GC seems to hijack traffic to Baidu, so it is possible that Baidu might not be working with the attacker. It hijacks the request for a javascript file and returns a malicious one that tells the browser to request things on Github.
- According to CitizenLab, the Chinese government is probably behind this attack.

**<a href="https://www.cloudflare.com/learning/ddos/famous-ddos-attacks/">Cloudflare</a>**

Was at that time the biggest DDoS attack ever.
