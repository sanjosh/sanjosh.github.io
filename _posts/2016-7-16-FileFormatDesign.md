---
layout: post
title: File Format design
---

Points to consider while designing a file format

* prefer self-describing files (no external metadata)
* checksum
* version number
* magic bytes (at beginning or end)
* creation date
* encoding for dates, text, binary data must follow some standard.
* endian (little or big)
* use TLV (tag-length-value) ?
* use PNG idea - have series of chunks, each with a type, length and data.  Unrecognized chunks can be ignored.

References
* <https://en.wikipedia.org/wiki/File_format>
* <https://www.w3.org/TR/PNG/>
* <http://www.magicdb.org/filedesign.html>
* <http://www.perlmonks.org/?node_id=491321>
* <http://stackoverflow.com/questions/323604/what-are-important-points-when-designing-a-binary-file-format>
