---
layout: post_1
title: 04 - Sofware License
date: 2019-04-20 -0400
categories: podcast
anchor: https://anchor.fm/randomly-typed/embed/episodes/Software-Licenses-e3psmk/a-adi4k1
description: "Can I take your code and sell it? We discuss the variety of available licenses and whether they make sense in our current technological landscape."
permalink: /4.html
---

## License <span class="footnote"></span>
- It is the authorization to do something.
- The license might cost something.
- Might be used to allow someone to use a patented invention or to use a software
- Governed by intellectual property laws

## Intellectual property <span class="footnote"></span>
- Intellectual property (IP) is a category of property that includes intangible creations of the human intellect.
- Intellectual property encompasses two types of rights; industrial property rights like (trademarks, patents, designations of origin and industrial designs) and copyright
  - Trademark : Brand names, product : iPhone’s name
  - Patents : One click buy
  - designations of origin: Protect the country's highest quality produce
  - industrial designs: Feel and look of iPhones
  - Copyright :  is a legal right that grants the creator of an original work exclusive rights. Eg. Music
- The objectives of intellectual property law is to encourage the creation of inventions.
  - For a limited amount of time, the creator should be protected from other people copying him.
  - These incentives are should stimulate innovation and contribute to the progress of countries.
  - For example, R&D expensive to create new drug. If the company couldn’t make money out of it since every other companies could copy, they would not put all the R&D money.

## Software licenses <span class="footnote"></span>
- Legal instrument governing the use or redistribution of softwares.
- In the US, this protect the source code and the compiled version
- Many different types, normally on a scale between public domain and trade secrets
- FOSS license let people see the source and modify it


- **Public domain**
- **Copyleft (GPL family)**
  - They require all modifications, and any software based on the open source component, even in a small part, to be released under an open source license.
  - Examples : Linux kernel.
    - The success of Linux is in part linked to its GPL license. Every improvement done to it needs to be open sourced.
- **Permissive license (BSD, MIT, APACHE2)** <span class="footnote"></span>
  - allows users of the software to distribute, modify, or otherwise use software for any purpose, as long as the user complies with the license terms.
  - Gives attribution back to the author
  - Easier commercial adoption
  - Example Apache 2 : software users can’t initiate litigation over patent infringement (and if so, they lose their license).
  - Facebook in 2014, BSD+Patents, specifies that if you sue the creator of the software for patent infringement, even if unrelated to the current open source software, you lose the patent license granted by the creator. Using software under BSD+Patents can endanger a company’s own patents, and can be frowned upon if it is acquired by a larger company. Switched to MIT.
  - Changing license is not retroactive
  - Examples : BSD kernel -> Darwin, macOS and iOS layered upon Darwin. Microsoft took some code from the BSD kernel for their TCP/IP stack
- **Freeware**
  - Free to use and copy
  - Most of the time, don’t have access to source
  - Can’t modify or sublicense
  - Example : Truecrypt. Source available freeware. After end of life was announced, many teams fork the project. Weird licensing issue here.
- **Proprietary license**
  - You pay for it and are allowed to use it according to some limits
  - Example : Windows. Can install it on one computer. Some weird edge cases, what’s a computer? Swap hard drive…
- **Trade secrets**
  - Google.com
  - Might be allowed to access it
- **SSPL (server side public license)**
  - Mongo added new license
  - which stipulates that anyone offering MongoDB as a cloud service must release the code written to enable that managed service as an open-source project of its own. <span class="footnote"></span>
    - AWS started to offer new DocumentDB after the new license.
    - Emulate mongo 3.6 responses (3.6 before license change)
  - Mongo is a company that tries to survive by selling hosted infrastructure of their software.
  - Dropped from red hat
- **RSAL** <span class="footnote"></span>
  - Redis is BSD, but has some modules distributed under RSAL
    - Cloud provider can’t offer those modules
  - Opened core
- According to Github in 2018, Microsoft and Google are the biggest contributors. <span class="footnote"></span>
- No license: Code without an explicit license is protected by copyright and is by default All Rights Reserved. <span class="footnote"></span>

<span class="footnotes">
  <a href="https://en.wikipedia.org/wiki/License">[1] https://en.wikipedia.org/wiki/License</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Intellectual_property">[2] https://en.wikipedia.org/wiki/Intellectual_property</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Software_license">[3] https://en.wikipedia.org/wiki/Software_license</a> <br/>
  <a href="https://snyk.io/blog/mit-apache-bsd-fairest-of-them-all/">[4] https://snyk.io/blog/mit-apache-bsd-fairest-of-them-all/</a> <br/>
  <a href="https://www.geekwire.com/2019/amazon-web-services-calls-mongodbs-licensing-bluff-documentdb-new-managed-database/">[5] https://www.geekwire.com/2019/amazon-web-services-calls-mongodbs-licensing-bluff-documentdb-new-managed-database/</a> <br/>
  <a href="https://www.zdnet.com/article/redis-labs-drops-commons-clause-for-a-new-license/">[6] https://www.zdnet.com/article/redis-labs-drops-commons-clause-for-a-new-license/</a> <br/>
  <a href="https://www.theregister.co.uk/2019/02/22/redis_labs_changes_license_funding_60m/">[7] https://www.theregister.co.uk/2019/02/22/redis_labs_changes_license_funding_60m/</a> <br/>
  <a href="https://medium.freecodecamp.org/the-top-contributors-to-github-2017-be98ab854e87">[8] https://medium.freecodecamp.org/the-top-contributors-to-github-2017-be98ab854e87</a> <br/>
  <a href="https://www.infoworld.com/article/2615869/github-needs-to-take-open-source-seriously.html">[9] https://www.infoworld.com/article/2615869/github-needs-to-take-open-source-seriously.html</a> <br/>
</span>
