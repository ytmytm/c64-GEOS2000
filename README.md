

GEOS KERNAL v2.0 - commented source code
========================================
by Maciej 'YTM/Elysium' Witkowiak
6-6-99, 18-8-99, 18/29-2-2000, 2014



# DESCRIPTION
This archive contains FULL source code of GEOS KERNAL v2.0, english version.
It is identical to original in critical points but the code is revised,
optimized, reorganized and first steps towards modularizing are made.



# DISCLAIMER
This package comes from full disassembling of GEOS KERNAL. I did it for my
own pleasure and purposes in my spare time. It is meant for customizing the
code and not for making big bucks on it. If you want to use GEOS KERNAL
generated from these sources you need to have an original copy of GEOS,
because you can do nothing without DeskTop, applications and so.

Although I have throughly tested it I cannot guarantee that it will work on
any hardware configuration and with any applications.



# REQUIREMENTS
The only tool required is ACME (version at least 0.07). It may be obtained
from:
http://sourceforge.net/projects/acme-crossass/
Bash shell is helpful and existance of c1541 from VICE package will be good
too. You will probably want to have pucrunch from 
https://github.com/mist64/pucrunch
Base distribution of these sources is intended for UNIX systems, but ACME in
DOS will do too.
To compile the kernel simply do
```
make
```
It will work flawlessly if you have c1541 and pucrunch. Anyway if you only
have ACME make will stop after assembling the system and you will have
geoskernal.bin file ready for loading into c64 and SYS $5000.


# CUSTOMIZATION

Look into inc/equ.inc file - there are many true/false defines, you are free
to change them. But read the comments. You can compile-in input and disk
drivers so right after boot you will have your drivers (and you can boot from
1571/81 without any problems). In case that input driver is compiled into
KERNAL you have to delete all input driver files from boot disk, because
DeskTop will try to load the first one overriding compiled driver.
If you have C128 it is worth to enable 2MHz support - CPU is warped into 2MHz
on the border. This is better than add-on that I saw somewhere, because my
version will not flicker anytime and that add-on will not work with this
kernal. (not a single application that modifies GEOS KERNAL directly will not
work).



# *NIX INSTALL

Use Makefile for creating a binary file and a disk image with it. It will
be placed on top of the source tree.
'geoskern.bin' is the binary file
'geoskern.puc' is the crunched binary (just RUN it)
'geosboot.d64'   is the disk image

If you don't have pucrunch simply move geoskernal.bin to c64 disk and treat it
with any squeezer/cruncher. Even charpackers will be good. Let's say
that you have crunched the KERNAL and saved the file as GEOS.PRG. From now on
you can boot the system by simply loading and RUNning this file.

To make a new boot disk:
Prepare a blank disk, copy DeskTop, auto-execs (Configure etc.) there,
your input driver (if it is different than that compiled into KERNAL), printer
driver and whatever you want. Oops, I would have forget - of course copy your
packed KERNAL there also.



# *NIX CLEAN
```
make clean
```
will remove all output files from the source tree.


# MS-DOS INSTALL

Execute MAKEGEOS.BAT file, it will try to assemble the whole thing. I don't have pucrunch for
DOS, so you will have uncompressed output file - geoskern.bin. Move it to a disk (image) and
compress on c64 or execute - start and load address is $5000 - e.g.
```
LOAD "GEOSKERN.BIN",8,1
SYS20480
```

# THE SOURCES

Source code is organized in a specific way. You can browse through it easier
by using some keypoints:

## 1) Labels
All global labels are identical to those from geosSym and geosMac files. All
OS_JUMPTAB functions are preceded with '_'. For example EnterDeskTop is placed
in jumptab as:
```
EnterDeskTop		JMP _EnterDeskTop
(...)
_EnterDeskTOp		; code for handling this function
```

All other labels are meant to descript the purpose of a subroutine. It was not
always possible, so you may find some UNK_xxx, xxxHelp_xx and lots of
procedures with the same name but different number e.g. Font11, Font12 etc.
In current version all labels are global and these which should be local are
made by abbreviation of the subroutine with a number on its end.
In future releases it will be fixed and named ACME !zone(s) will be used.

## 2) Indentation
This goes like that:
```
		[tab2]				[tab6]
Label		LDA #0				;$xxxx
```

CPU opcodes are always on 1st or 2nd tab. If it is 1st tab position, it means
that the purpose of current/called subroutine/memory location is unknown.
Comments are always on 6th tab position. The source is full of ;$xxxx
comments. It is relict from disassembling the KERNAL - those marks helped me
a lot when debugging. Currently the values there are wrong because code is
optimized and reorganized. They will be removed in future releases.

# SOURCE TREE

./bin	-	all binary files goes there
./inc	-	all include files
./src	-	all source files

subdirectories of ./bin and ./src
./drv	-	disk drivers code/binary
./input	-	input drivers code/binary

Description of sources can be found at top of each file.



# COMMENTS
Well, the sources are not yet commented very much, but the labels are very
descriptive (as for me anyway). You should obtain the GEOS Programmer's
Reference Book (by Alexander Boyce) for full description of all jumptab
functions and many GEOS data structures. This document is available in text
and HTML format from
ftp.funet.fi/pub/cbm/[somewhere...]
ftp.elysium.pl/tools/systems/geos/docs [or /programming]



# AUTHOR
And reverse-engineer :}
Maciej Witkowiak
ytm@elysium.pl


# END WORDS
Have fun!
