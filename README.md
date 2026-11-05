# apex legends full pe section dump

dumped every section of r5apex.exe on the current version of the game. everything u need to make a cheat for apex is in here. the whole engine, what it does, whatever the anti cheat left behind, and every offset is sitting in these files. dig through it and find ur bypass

## the files

**headers.bin** : the pe headers of r5apex.exe. mz stub, pe sig, optional header, section table, all the data directories. tells u the image base and where every section goes

**data.bin** : the .data section, biggest file at 13mb. all the globals and engine data live here, most offsets u care about point into this one

**rdata.bin** : the .rdata section, 6.7mb. all the strings, vtables, imports and convars. most useful file for reversing, every engine string and respawn endpoint is in here

**rdata2.bin** : a second tiny rdata section, 3kb of extra pointer pairs

**pdata.bin** : the .pdata section, exception unwind info. gives u every functions start and end address, good for mapping the binary

**fptable.bin** : 512 bytes of raw function pointers

**reloc.bin** : the .reloc section, base relocations. every spot that gets patched when aslr slides the base around

**rsrc.bin** : the .rsrc section, resources. icon, manifest, version info

**sec9.bin** : section 9, still encrypted. the packed part of the exe, good luck

## using it

grab the image base and section rvas out of headers.bin, drop each bin back at its rva and u got the whole exe rebuilt in ida or whatever u use. or just work the sections raw, rdata.bin and data.bin are where the good stuff is
