# every file explained

## sections

the actual sections out of r5apex.exe, dumped from the current version

**sections/headers.bin** : pe headers of r5apex.exe. image base, section table, data directories. this tells u where every other bin goes

**sections/data.bin** : the .data section, 13mb. globals and engine data, most offsets point into here

**sections/rdata.bin** : the .rdata section, 6.7mb. strings, vtables, imports, convars. the main file for reversing

**sections/rdata2.bin** : second tiny rdata section, 3kb of pointer pairs

**sections/pdata.bin** : the .pdata section, unwind info. every functions start and end address

**sections/fptable.bin** : 512 bytes of raw function pointers

**sections/reloc.bin** : the .reloc section, base relocations for when aslr moves the base

**sections/rsrc.bin** : the .rsrc section, resources. icon, manifest, version info

**sections/sec9.bin** : section 9, still encrypted. the packed part of the exe

## anticheat

**anticheat/preloader.dll** : the unsigned EA SPEAR anticheat preloader. loads before the game, maps memory, does its checks. throw it in ida

**anticheat/preloader_imports.txt** : every import in preloader.dll. mostly raw ntdll, NtAllocateVirtualMemory, NtMapViewOfSection, NtProtectVirtualMemory, manual mapping all day

**anticheat/preloader_strings.txt** : every string in it. got /work/preloader.pdb and the EA SPEAR AntiCheat Engineering string in there

## recon

**recon/depot.txt** : respawns internal source paths leaked out of the pdb. c:\depot\r5-310\... shows the whole source tree, engine files, protobuf defs

**recon/fingerprint.json** : the machine fingerprint the game sends up. mid, bsn, msn, hsn, gid, mac, timestamps. the hwid schema, values redacted

**recon/hosts.txt** : every ea and respawn domain the game talks to. blocklist or mitm

**recon/oauth.txt** : oauth format strings for ea login, auth and token request templates

**recon/cfg_strings.txt** : string dump of the exe. exe names, section names, embedded manifest
