---
layout: post
title:  "This 1301 byte PDF file has 2 million pages"
date:   2021-04-12 19:44:00 +0200
tags:   pdf
---

This innocent looking [1301 byte .PDF](/files/dont_open_this.pdf) file actually
has 2 million pages. The file only has 10 objects, of which 7 are page groups
that recursively contain 8 copies of the next page group for a total of 8^7 =
2097152 copies of the same single page.

Firefox and Edge appears to get stuck allocating gigabytes of memory and
will eventally crash. Impressively,
[SumatraPDF](https://www.sumatrapdfreader.org) actually handles the file very
well.

Adobe Acrobat Reader does not render the PDF file, as it does not seem to
support having the same `Page` object used more than once. Checking the
[specification](http://wwwimages.adobe.com/www.adobe.com/content/dam/acom/en/devnet/pdf/pdfs/PDF32000_2008.pdf)
did not immediately yield a clear answer to whether page reuse is legal. The
entire structure is made of indirect object references, and I did not find any
indication that an object can't be reused more than once.
