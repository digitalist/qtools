#qtools usage examples

This document contains examples of practical tasks solved with qtools

## Replace modem IMEI

IMEI is stored at nvram address 0x226. The problem is this addres has a write-once attribute. Meaning they write it once during production and all consequent writes to this cell will silently fail — even without error message. We'll overcome this restriction, but we have to go the same path nvram and EFS are produced. 

Here's an example for ZTE MF823/825, other modems may require a slightly different approach - i.e. only ZTE
modems use `config` file


1. Download all nvram cells/data from moded:

./qnvram -ri

2. Download` config`  file (For ZTE-modems):

./qefs -gf confg

3. Switch modem to upload mode and upload NPRG, like this (for ZTE823):

./qcommand -e -c"c 3a"
./qdload -i loaders/NPRG9x15p.bin

Commands are dependant on chipset/model.

4. Clear EFS partition. Determine its starting block & size using qrflash, then erase through qwdirect:

./qrflash -s@ -m
./qwdirect -b<start> -c<len>

5. Reboot modem (switch on/off power and usb).
6. Rewrite IMEI with your value:

./qnvram -j 834001432784560

7. Return other nvram cells to their initial state:

./qnvram -wa

1. Write `config` file back (if it was present, see above)

./qefs -wf config /

That's all.  If device is in a factory mode (with ttyUSB-ports), switch it to working mode with `at+zcdrun=f` command and reboot it. 