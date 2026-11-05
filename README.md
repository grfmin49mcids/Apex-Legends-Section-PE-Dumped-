# apex legends full pe section dump

dumped every section of r5apex.exe on the current version of the game. everything u need to make a cheat for apex is in here. the whole engine, what it does, the actual anticheat preloader, and every offset is sitting in these files. dig through it and find ur bypass

## the section dumps

**headers.bin** : the pe headers of r5apex.exe. mz stub, pe sig, optional header, section table, all the data directories. tells u the image base and where every section goes

**data.bin** : the .data section, biggest file at 13mb. all the globals and engine data live here, most offsets u care about point into this one

**rdata.bin** : the .rdata section, 6.7mb. all the strings, vtables, imports and convars. most useful file for reversing, every engine string and respawn endpoint is in here

**rdata2.bin** : a second tiny rdata section, 3kb of extra pointer pairs

**pdata.bin** : the .pdata section, exception unwind info. gives u every functions start and end address, good for mapping the binary

**fptable.bin** : 512 bytes of raw function pointers

**reloc.bin** : the .reloc section, base relocations. every spot that gets patched when aslr slides the base around

**rsrc.bin** : the .rsrc section, resources. icon, manifest, version info

**sec9.bin** : section 9, still encrypted. the packed part of the exe, good luck

## the good stuff

**preloader.dll** : the actual anticheat preloader, unsigned. this is the EA SPEAR anticheat module that runs before the game, maps stuff into memory and does its checks. this is the thing u wanna tear apart

**preloader_imports.txt** : every import in preloader.dll. almost all raw ntdll, NtAllocateVirtualMemory, NtMapViewOfSection, NtProtectVirtualMemory, classic manual mapping

**preloader_strings.txt** : every string in the dll. got the pdb path /work/preloader.pdb and the EA SPEAR AntiCheat Engineering string right in it

**depot.txt** : respawns internal source paths leaked from the pdb, c:\depot\r5-310\... the whole source tree layout. engine files, protobuf defs, all of it

**fingerprint.json** : the machine fingerprint the game sends up. mid, bsn, msn, hsn, gid, mac, timestamps. this is the hwid schema that gets u banned, values are redacted but the whole structure is there

**hosts.txt** : every ea and respawn domain the game talks to. stryder endpoints, accounts, stats, all of it. blocklist or mitm, ur call

**oauth.txt** : the oauth format strings for ea login, auth and token request templates

**cfg_strings.txt** : string dump of the exe. exe names, section names, embedded manifest

every file is also in FILE_INDEX.md if u want the quick list

## using it

grab the image base and section rvas out of headers.bin, drop each bin back at its rva and u got the whole exe rebuilt in ida or whatever u use. or just work the sections raw, rdata.bin and data.bin are where the good stuff is. preloader.dll is small and unsigned so throw it straight in ida too
