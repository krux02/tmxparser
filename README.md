# tmx-parser

This is a library for parsing the maps generated by
[Tiled Map Editor](https://github.com/bjorn/tiled/).

The TMX format is based upon XML and may contain compressed and encoded tile
data to save memory and reduce file sizes. This parser uses the
[TinyXML](http://www.grinninglizard.com/tinyxml/) library and its DOM interface
to parse TMX files.

An example file is provided to understand how to use the library.

## Features

 * Conformity with the [TMX specification page](https://github.com/bjorn/tiled/wiki/TMX-Map-Format).
 * Decodes and decompresses tile data.
 * Can parse properties as both integers, real numbers and literals (strings).
 * Can parse the map file when stored in memory.
 * Does not rely on any graphics library.

## Dependencies

 * zlib
 * TinyXML

## Installation

```
make -f Makefile.linux
sudo make -f Makefile.linux install
```