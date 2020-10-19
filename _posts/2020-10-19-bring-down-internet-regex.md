---
layout: "post_1"
title:  "30 - How to Bring Down the Internet with Regex"
date:   2020-10-19
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/30---How-to-Bring-Down-the-Internet-with-Regex-el9shu"
description: "JS and Lance chat about a couple of interesting and very public incidents of a regular expression unexpectedly causing major outages at well-known software companies. We walk through exactly how these incidents happened and discover how easy it is to write a regex with no time complexity guarantees."
permalink: /30.html
---
# CLOUDFLARE INCIDENT <span class="footnote"></span>

- July 2nd, 2019
- What happened:
  - All traffic on the Cloudflare network worldwide ground to a halt.
  - Pretty much every browser user saw a 502 Bad Gateway on most sites for ~30-60 minutes
- Affected their Web Application Firewall:
  - Cloudflare has their own WAFs developed in Lua.
  - Protects web applications from attacks like CSS, SQL injection by monitoring HTTP traffic
    - Layer 7 in the OSI model: application layer
  - Acts as a reverse-proxy, in that it hides clients from the server
- All CPUs were exhausted on all machines that handle HTTP traffic on the Cloudflare network worldwide.
- A “minor fix” was deployed to a single WAF policy with a change to a regular expression for XSS detection
  - TLDR: when you trick a website into displaying a malicious script you control to other users
  - Go check out the blog post, they include the regular expression there, so well written
- Normal changes go through a rigorous slow deployment process, but since WAF policies can require urgent deployment, they’re pushed to a key-value store and go live in seconds. 
- They deployed it to a “simulation” mode on their clusters in which real customer traffic passes through the new WAF rule, but nothing is blocked. Used to assess the false-positive/negative rate of a new policy before deploying it.
  - Unfortunately, even when simulating a new rule, it needs to _execute_ that new rule.
- It contained a change which caused a backtrack, which is much more CPU-intensive
  - The Lua WAF uses PCRE (Perl Compatible Regex expressions).
    - There are lots of different kinds of regex engines. Some allow features that others don’t, mostly for performance reasons. PCRE allows backtracking because it unlocks some features that other regex engines can’t express, but it comes at a significant performance cost with no complexity guarantees
      - Let’s talk about language classes and regexes in a next episode
- They accidentally removed a check for CPU exhaustiveness in WAFs during a refactor only weeks prior and didn’t have benchmarking as part of their test suite. 

## Resolution:
- Able to rollback but had issues since accessing their own systems was difficult with the incident, and a bunch of security credentials had timed out at the same time.
- Add the CPU exhaustiveness checks and tests
- Manually inspect all 3868 regexes for backtracking
- Switch to a different regex engine


## Backtracking:
- Warning: I’m not a regex engine, actual details may be wrong, but here’s the intuition behind it.
- `.*.*=.*` asks a regex engine to match “anything, followed by anything”
- `.*` matches zero or more characters, greedily (aka. As much of the pattern as possible)
- Test case: `x=x` matches `.*.*=.*`, but it takes 23 steps for the match to happen.
    - The first `.*` matches `x=x`.
    - The second `.*` matches nothing
    - The `=` can’t be matched, so it needs to _backtrack_ to the first `.*`
    - The first `.*` then tries to match `x=`.
    - The second `.*` matches `x`
    - The `=` can’t be matched, so it needs to  _backtrack_ to the first `.*`
    - The first `.*` then tries to match `x`
    - The second `.*` matches `=x`
    - The `=` can’t be matched, so it needs to _backtrack_ to the first `.*`
    - …
- `x=x` -> 23 steps
- `x=xx` -> 33 steps
- `x=xxx` -> 45 steps
- With 20 `x`, 555 steps
- This is exponential growth.
- The fact that it allows this backtracking is why PCRE has no complexity guarantees
- Sometimes, a fix is to use lazy matches instead of greedy. Doing `.*?` acts the engine to match anything, but the least amount of characters, before moving on. But it still has no complexity guarantees.
- It turns out the only real solution is to rewrite your regex, and for some regexes, that will be impossible, because some strings can never be matched without backtracking.
- Formal language theory in a future episode
- Regex engines without features like backtracking can only express regular languages, which is limited.
- Eg. Take home exercise: try to write a regex which matches all non-empty even-length strings, the first half being `a`’s, the second half being `b`’s.

# Stackoverflow Incident <span class="footnote"></span>
- On july 20th 2016, SO was down for 34minutes.
> It took 10 minutes to identify the cause, 14 minutes to write the code to fix it, and 10 minutes to roll out the fix to a point where Stack Overflow became available again.
  - Triggered by a post and was triggering the issue on each home page view.
  - The post was: “play happy sound for player to enjoy.” followed by roughly 20_000 spaces and something else afterward.
  - Regex could have been `\s+$`. Used to trim whitespaces
> the Regex engine will start at the first space, check that it belongs to the \s character class, move to the second space, make the same check, etc. After the 20,000th space, there is a different character, but the Regex engine expected a space or the end of the string. Realizing it cannot match like this it backtracks, and tries matching \s+$ starting from the second space, checking 19,999 characters. The match fails again, and it backtracks to start at the third space, etc.
> So the Regex engine has to perform a “character belongs to a certain character class” check (plus some additional things) 20,000+19,999+19,998+…+3+2+1 = 199,990,000 times, 

> (performance is O(n²))

# References:
https://regexcrossword.com/
https://stackoverflow.com/questions/38484433/join-tiles-in-corona-sdk-into-one-word-for-a-breakout-game-grid

<span class="footnotes">
  <a href="https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/">[1] https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/</a>
  <a href="https://stackstatus.net/post/147710624694/outage-postmortem-july-20-2016">[2] https://stackstatus.net/post/147710624694/outage-postmortem-july-20-2016</a>
</span>
