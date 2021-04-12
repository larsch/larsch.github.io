---
layout: post
title:  "This 1301 byte PDF file has 2 million pages"
date:   2021-04-12 19:44:00 +0200
tags:   pdf
---

This innocent looking [1301 byte .PDF](/files/dont_open_this.pdf) file actually
has 2 million pages and will cause Firefox and Bing to go out of memory and
crash. Impressively, [SumatraPDF](https://www.sumatrapdfreader.org) actually
handles it very well.

The file only has 10 objects, of which 7 are page groups that recursively
contain 8 copies of the next page group for a total of 8^7 = 2097152 copies of
the same single page.
