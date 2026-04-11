# Notorious

I use `MyPortIO.sys` as an example. This driver uses `MmMapIoSpace` to read and write memory, but it can only process a `DWORD` at a time.

You can easily replace it with any vulnerable driver you prefer.

## How it works

The method involves changing the pointer in `SeCiCallbacks`. When Windows attempts to validate the certificate of a driver, it will call this function. By changing it to `ZwFlushInstructionCache` (a function that always returns `TRUE`), we can successfully bypass this check. Both of these functions reside within `ntoskrnl.exe`.

---

## Why not just simply modify the DSE value?

Some pre-loaded anti-cheat systems may actively monitor or track the DSE (Driver Signature Enforcement) value, making it unsafe to modify directly.

## Acknowledgements

Special thanks to:
- **TheCruZ** - [kdmapper-SymbolForPdb](https://github.com/TheCruZ/kdmapper/tree/master/SymbolsFromPDB)
- **jonomango** - [SuperFetch](https://github.com/jonomango/superfetch)
