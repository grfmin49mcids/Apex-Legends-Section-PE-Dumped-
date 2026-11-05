# every file explained

## the section dumps

these are the actual sections out of r5apex.exe, dumped from the current version

**headers.bin** : pe headers of r5apex.exe. image base, section table, data directories. this tells u where every other bin goes

**data.bin** : the .data section, 13mb. globals and engine data, most offsets point into here

**rdata.bin** : the .rdata section, 6.7mb. strings, vtables, imports, convars. the main file for reversing

**rdata2.bin** : second tiny rdata section, 3kb of pointer pairs

**pdata.bin** : the .pdata section, unwind info. every functions start and end address

**fptable.bin** : 512 bytes of raw function pointers

**reloc.bin** : the .reloc section, base relocations for when aslr moves the base

**rsrc.bin** : the .rsrc section, resources. icon, manifest, version info

**sec9.bin** : section 9, still encrypted. the packed part of the exe

## the anticheat stuff

**preloader.dll** : the unsigned EA SPEAR anticheat preloader. loads before the game, maps memory, does its checks. throw it in ida

**preloader_imports.txt** : every import in preloader.dll. mostly raw ntdll, NtAllocateVirtualMemory, NtMapViewOfSection, NtProtectVirtualMemory, manual mapping all day

**preloader_strings.txt** : every string in it. got /work/preloader.pdb and the EA SPEAR AntiCheat Engineering string in there

## the recon files

**depot.txt** : respawns internal source paths leaked out of the pdb. c:\depot\r5-310\... shows the whole source tree, engine files, protobuf defs

**fingerprint.json** : the machine fingerprint the game sends up. mid, bsn, msn, hsn, gid, mac, timestamps. the hwid schema, values redacted

**hosts.txt** : every ea and respawn domain the game talks to. blocklist or mitm

**oauth.txt** : oauth format strings for ea login, auth and token request templates

**cfg_strings.txt** : string dump of the exe. exe names, section names, embedded manifest
