# qtools
Tools for working with flash memory  of modems on a Qualcom chipset

It contains utilities and some patched firmware loaders

`qcommand` - an interactive shell for entering commands via command port, replaces horribly unusable `revskills`
        Allows byte-level input of command packets, memory editing, read/view every flash sector
           
`qrmem` - for reading a dump of device address space

`qrflash` - flash-reader. Can read a range of blocks or partitions using partition map.

`qwflash` - QPST-like utility for wirting partition images via `user partitions` loader mode 

`qwdirect` - raw/direct writing of flash blocks w/wo OOB [Out of band] through controller ports (without loader)

`qdload` - loader for loaders. Requires the modem to be in `download mode` or `PBL` (`primary boot loader`) mode.

`dload.sh` - switches device to download mode, uploads a provided loader 


These utilities require patched loaders, which are located in `loaders` directory, patch source is located in 
`cmd_05_write_patched.asm`
