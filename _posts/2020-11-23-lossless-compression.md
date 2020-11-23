---
layout: "post_1"
title:  "32 - Lossless compression algorithms"
date:   2020-11-23
categories: podcast
anchor: "https://anchor.fm/randomly-typed/embed/episodes/32---Lossless-compression-algorithms-emt9j0"
description: "Lance and JS try to make things smaller! In this episode, we explore how to compress information efficiently in a variety of different ways with different tradeoffs."
permalink: /32.html
---
# Types of compressions
- Lossless
  - Generic
- Lossy
  - Domain specific

# Algos <span class="footnote"></span>
## Dictionary coding <span class="footnote"></span>
- Also sometimes known as a substitution coder

### Static
With a static dictionary coding, you have a predefined dictionary of common patterns. It searches in the input text and if it finds a match from the dictionary, it replaces the match in the input text by a reference to the dictionary.
- Example : Restaurant menu
- That’s what brotli does. It has a 120kb dictionary of common strings used on the Internet.
- Those algorithms are not/less general purpose since you need a pre-built dictionary which will be domain specific. It has the advantage that the dictionary doesn’t need to be transmitted.

### Dynamic
Lempel-Ziv algorithms use dynamic dictionaries.

## Lempel-Ziv
- Really influential 
- Also known as LZ77 in 1977
- There’s many variance and was the base to many data compression research
- Among others, it influenced GIF and DEFLATE which is used for PNG and ZIP

### LZ77
Keep a sliding window (which is the dictionary) of seen data and when there’s an already seen pattern it replaces it with 2 numbers. How many characters to look back and how many characters to copy.

ABCABD -> ABC<3,2>D

### LZ78 <span class="footnote"></span>
LZ77 had the problem of needing to optimize parameter (the size of the window). Too small won’t get good compression. Too big, will be slow. To solve that problem LZ78 store the data in a dictionary. The dictionary is a non-binary tree. Every leaf contains a character.

### Lempel-Ziv-Storer-Szymanski (LZSS)
Just like LZ77, but will only replace when there’s a match if the marker is smaller than the match. This will prevent the creating a bigger file.

## Huffman coding <span class="footnote"></span>
- Published in 1952 in "A Method for the Construction of Minimum-Redundancy Codes".
- There’s many implementations and improvements, but normally this is a multi steps algorithm.
- Use a variable-length coding table derived from the frequency of symbols in the input data (letters for example). The table can be derived from the frequency of occurrence for each symbol.
- The “trick” with the algorithm is that symbols that are present more often are represented with lesser bits.
> “Huffman's method can be efficiently implemented, finding a code in time linear to the number of input weights if these weights are sorted.”
### Example from Wikipedia
> "this is an example of a huffman tree". The frequencies and codes of each character are below. Encoding the sentence with this code requires 135 (or 147) bits, as opposed to 288 (or 180) bits if 36 characters of 8 (or 5) bits were used.

| Char | Freq | Code |
| --- | --- | --- |
| space | 7 | 111 |
| a | 4 | 010 |
| e | 4 | 000 |
| f | 3 | 1101 |
| h | 2 | 1010 |
| i | 2 | 1000 |
| m | 2 | 0111 |
| n | 2 | 0010 |
| s | 2 | 1011 |
| t | 2 | 0110 |
| l | 1 | 11001 |
| o | 1 | 00110 |
| p | 1 | 10011 |
| r | 1 | 11000 |
| u | 1 | 00111 |
| x | 1 | 10010  |

## Arithmetic Coding <span class="footnote"> </span><span class="footnote"></span> 
- Really different than other methods.
- Normally used to encode strings.
- It represents the encoded string with a number between 0 and 1.
### Example
Follow exemple from https://go-compression.github.io/algorithms/arithmetic/.

- Can send any value in the interval.
- To decompress you “follow” the inverse path.

- Two big problems is that normally we don’t have arbitrarily precise floats, but when we do operations on them are pretty slow.
- There’s many variants.
  - Some don’t need arbitrarily precise numbers.

# Web <span class="footnote"></span>
>  gzip: An encoding format produced by the file compression program "gzip" (GNU zip) as described in RFC 1952. This format is a Lempel-Ziv coding (LZ77) with a 32 bit CRC.

 > compress: The encoding format produced by the common UNIX file compression program "compress". This format is an adaptive Lempel-Ziv-Welch coding (LZW).
[...]
- LZW is an improvement on LZ78 with variable width code similar to Huffman coding. <span class="footnote"></span>

> deflate: The "zlib" format defined in RFC 1950 in combination with the "deflate" compression mechanism described in RFC 1951.
> which uses a combination of a variation of LZ77 (Lempel–Ziv 1977) and Huffman coding <span class="footnote"></span>

## Brotli
Brotli is now also supported.
> Brotli is a data format specification for data streams compressed with a specific combination of the general-purpose LZ77 lossless compression algorithm, Huffman coding and 2nd order context modelling. Brotli is a compression algorithm developed by Google and works best for text compression. <span class="footnote"></span>
- As mentioned, it comes with a 120kb dictionary of common strings used on the Internet.
- Was added to HTTP in 2015
- According to a research from Akamai <span class="footnote"></span> looking at the top 1000 URLs on the web
  - HTML Brotli Improvement over GZIP, Median 21%
  - JS Brotli Improvement over GZIP, Median 14%
  - CSS Improvement over GZIP, Median 17%

## Usage <span class="footnote"></span> (2019)

| Algorithm | Usage |
| --- | --- |
| No Text Compression | 62.87% |
| Gzip | 29.66% |
| br | 7.43% |
| Deflate | 0.02% |

<span class="footnotes">
  <a href="https://go-compression.github.io/">[1] https://go-compression.github.io/</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Dictionary_coder">[2] https://en.wikipedia.org/wiki/Dictionary_coder</a> <br/>
  <a href="https://medium.com/@dbudhrani/how-data-compression-works-exploring-lz78-e97e539138">[3] https://medium.com/@dbudhrani/how-data-compression-works-exploring-lz78-e97e539138</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Huffman_coding">[4] https://en.wikipedia.org/wiki/Huffman_coding</a> <br/>
  <a href="https://go-compression.github.io/algorithms/arithmetic/">[5] https://go-compression.github.io/algorithms/arithmetic/</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Arithmetic_coding">[6] https://en.wikipedia.org/wiki/Arithmetic_coding</a> <br/>
  <a href="https://tools.ietf.org/html/rfc2616">[7] https://tools.ietf.org/html/rfc2616</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Welch">[8] https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Welch</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Zlib">[9] https://en.wikipedia.org/wiki/Zlib</a> <br/>
  <a href="https://en.wikipedia.org/wiki/Brotli">[10] https://en.wikipedia.org/wiki/Brotli</a> <br/>
  <a href="https://blogs.akamai.com/2016/02/understanding-brotlis-potential.html">[11] https://blogs.akamai.com/2016/02/understanding-brotlis-potential.html</a> <br/>
  <a href="https://almanac.httparchive.org/en/2019/compression">[12] https://almanac.httparchive.org/en/2019/compression</a> <br/>
</span>
