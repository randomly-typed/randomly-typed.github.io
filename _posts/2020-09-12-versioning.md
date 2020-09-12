---
layout: "post_1"
title:  "28 - Software Versioning Schemes"
date:   2020-09-12
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/28---Software-Versioning-Schemes-ejd56f
description: "We’re back! JS and Lance are ready to talk about software versioning schemes. Who would have that boiling down complex software systems into a series of numbers would be so hard?"
permalink: /28.html
---

# Software Versioning
## Why
2 of the things that versioning formats are trying to balance are
- Being human friendly
- Being machine friendly

## Semver <span class="footnote"></span> <span class="footnote"></span>
Semver is trying to avoid falling into “dependency hell”.
- If the dependencies are not well defined you will necessarily get bitten at some point by upgrading a dependency that will break something in an unexpected way.
- According to their documentation, the inverse would be
> if the dependency specifications are too tight, you are in danger of version lock (the inability to upgrade a package without having to release new versions of every dependent package).

### Npm <span class="footnote"></span>
From the NPM documentation
> To keep the JavaScript ecosystem healthy, reliable, and secure, every time you make significant updates to an npm package you own, we recommend publishing a new version of the package with an updated version number [...] that follows the semantic versioning spec. Following the semantic versioning spec helps other developers who depend on your code understand the extent of changes in a given version, and adjust their own code if necessary.

<table>
  <tr>
    <td>First release</td>
    <td>New product</td>
    <td>Start with 1.0.0</td>
  </tr>
  <tr>
    <td>Backward compatible bug fixes</td>
    <td>Patch release</td>
    <td>Increment the third digit 1.0.1</td>
  </tr>
  <tr>
    <td>Backward compatible new features</td>
    <td>Minor release</td>
    <td>Increment the middle digit and reset last digit to zero 1.1.0</td>
  </tr>
  <tr>
    <td>Changes that break backward compatibility</td>
    <td>Major release</td>
    <td>Increment the first digit and reset middle and last digits to zero 2.0.0</td>
  </tr>
</table>

## No semver <span class="footnote"></span>
Semver tries to optimize for machine readability. A simple program can read the format string and understand if the new version of the dependency can be used. But that’s not optimal for humans.

Semver is trying to compress too much data in too few numbers.
- What’s a breaking change?
  - Do I need to reorder a parameter on one single function
  - Or do I need to rewrite my whole application?
- If this update will break 0.01% of the applications using the dependency, should it be a new major version? What about 10%?

Semver might give a false sense of safety to developers.  Version numbers should try to replace a good changelog entry.

## Systemd
When there’s a new release, they just increase the version number and it’s done. There’s no special meaning to the number other than it’s a new number and they don’t promise anything about compatibility.  The current version is 245.

## Calver <span class="footnote"></span>
Or also known as Calendar Versioning.
- Not trying to be as strict as semver
- Ubuntu using 20.04 (YY.MM). Since the beginning
- Windows use to be XP service pack 2
  - Moved to Windows 10 Threshold, Redstone, 19H1, 19H2, 20H1, 20H2, 21H1 <span class="footnote"></span>
- Unity used Semver-like until 5 and in 2017 they switched to calvar. So now it’s Unity 2020.1.1

## Fedora packages <span class="footnote"></span>
Fedora has an interesting challenge compared to the others we talked about since they are bundling other people softwares which might be using different ways of naming their versions.

> The overriding goal is to provide sequences of packages which are treated as updates by RPM’s version comparison algorithm while accommodating varied and often inconsistent upstream versioning schemes.

Their simple versioning scheme
> They consists of one or more version components, separated by periods. Each component is a whole number, [...]. The rightmost component can also include one or more ASCII letters, upper or lower case. The value of a component must never be reduced (to a value which sorts lower) without a component somewhere to the left increasing

They have a bunch of other parts in their versioning format to accommodate for more complex problems.

## TeX
TeX is a formatting system written by Donal Knuth.

> Since version 3, TeX has used an idiosyncratic version numbering system, where updates have been indicated by adding an extra digit at the end of the decimal, so that the version number asymptotically approaches π <span class="footnote"></span>

Knuth decided to do that to represent the fact that there will never be any new feature. Every new release will only fix bugs.

## Browsers
Firefox and Chrome are fighting over who has the biggest number. We were on Firefox 3 for multiple years, but starting at Firefox 4, they started to frequently release new versions with new version numbers. Now, the release dates for Firefox and Chrome are known in advance and are stable.

For example, we know that for Firefox approximately every month a new version starts in nightly, one is moved to beta and one is released.

## Linux
> The Linux kernel bumped the version number from 2.6.39 to 3.0.0, because the 39 was getting a bit large, and to commemorate Linux' 20th anniversary. <span class="footnote"></span>

> But I'd like to point out (yet again) that we don't do feature-based releases, and that "5.0" doesn't mean anything more than that the 4.x numbers started getting big enough that I ran out of fingers and toes. <span class="footnote"></span>

<span class="footnotes">
  <a href="https://docs.npmjs.com/about-semantic-versioning">[1] https://docs.npmjs.com/about-semantic-versioning</a> <br/>
  <a href="https://semver.org/">[2] https://semver.org/</a> <br/>
  <a href="https://docs.npmjs.com/about-semantic-versioning">[3] https://docs.npmjs.com/about-semantic-versioning</a> <br/>
  <a href="https://gist.github.com/jashkenas/cbd2b088e20279ae2c8e">[4] https://gist.github.com/jashkenas/cbd2b088e20279ae2c8e</a> <br/>
  <a href="https://calver.org/">[5] https://calver.org/</a> <br/>
  <a href="https://en.wikipedia.org/wiki/List_of_Microsoft_Windows_versions">[6] https://en.wikipedia.org/wiki/List_of_Microsoft_Windows_versions</a> <br/>
  <a href="https://docs.fedoraproject.org/en-US/packaging-guidelines/Versioning/">[7] https://docs.fedoraproject.org/en-US/packaging-guidelines/Versioning/</a> <br/>
  <a href="https://en.wikipedia.org/wiki/TeX">[8] https://en.wikipedia.org/wiki/TeX</a> <br/>
  <a href="https://softwareengineering.stackexchange.com/a/255201">[9] https://softwareengineering.stackexchange.com/a/255201</a> <br/>
  <a href="https://lkml.org/lkml/2019/3/3/236">[10] https://lkml.org/lkml/2019/3/3/236</a> <br/>
</span>
