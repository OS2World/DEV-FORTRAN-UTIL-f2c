#.SUFFIXES: .c .o
#CC = cc
#CFLAGS = -O
#SHELL = /bin/sh

##############
# static libs
#AR = ar
#RANLIB = ar sv
#A = a
#O = o
#CFLAGS = -s -O -DOS2 -DNON_UNIX_STDIO
##############
# dynamic libs
AR = emxomfar
RANLIB = emxomfar sv
A = lib
O = obj
CFLAGS = -Zomf -Zmtd -s -O -DOS2 -DNON_UNIX_STDIO
#CFLAGS = -Zdll -Zomf -Zmtd -mprobe -s -O -DOS2 -DNON_UNIX_STDIO	# for DLL
##############
EXE = .exe
.SUFFIXES:
.SUFFIXES: $(EXE) .$A .$O .c .h
CC = gcc -ansi -I..
ARFLAGS = rv
YACC = yacc
YFLAGS = -dv
##############
SHELL = ksh
SHELLFLAGS = -c
COMMAND = "$(CMNDNAME) $(CMNDARGS)"

.c.$O:
	$(CC) -c $(CFLAGS) $*.c
 
# compile, then strip unnecessary symbols
#.c.o:
#	$(CC) -c -DSkip_f2c_Undefs $(CFLAGS) $*.c
#	ld -r -x -o $*.xxx $*.o
#	mv $*.xxx $*.o

OBJ =	Version.$O backspace.$O close.$O dfe.$O dolio.$O due.$O endfile.$O err.$O \
	fmt.$O fmtlib.$O iio.$O ilnw.$O inquire.$O lread.$O lwrite.$O open.$O \
	rdfmt.$O rewind.$O rsfe.$O rsli.$O rsne.$O sfe.$O sue.$O typesize.$O uio.$O \
	util.$O wref.$O wrtfmt.$O wsfe.$O wsle.$O wsne.$O xwsne.$O
libI77.$A:	$(OBJ)
		$(AR) $(ARFLAGS) libI77.$A $?
		$(RANLIB) libI77.$A
install:	libI77.$A
	cp libI77.$A /usr/lib/libI77.$A
	$(RANLIB) /usr/lib/libI77.$A

#Version.$O: Version.c
#	$(CC) -c Version.c

# To compile with C++, first "make f2c.h"
f2c.h: f2ch.add
	cat /usr/include/f2c.h f2ch.add >f2c.h


clean:
	rm -f $(OBJ) libI77.$A

clobber:	clean
	rm -f libI77.$A

backspace.$O:	fio.h
close.$O:	fio.h
dfe.$O:		fio.h
dfe.$O:		fmt.h
due.$O:		fio.h
endfile.$O:	fio.h rawio.h
err.$O:		fio.h rawio.h
fmt.$O:		fio.h
fmt.$O:		fmt.h
iio.$O:		fio.h
iio.$O:		fmt.h
ilnw.$O:	fio.h
ilnw.$O:	lio.h
inquire.$O:	fio.h
lread.$O:	fio.h
lread.$O:	fmt.h
lread.$O:	lio.h
lread.$O:	fp.h
lwrite.$O:	fio.h
lwrite.$O:	fmt.h
lwrite.$O:	lio.h
open.$O:	fio.h rawio.h
rdfmt.$O:	fio.h
rdfmt.$O:	fmt.h
rdfmt.$O:	fp.h
rewind.$O:	fio.h
rsfe.$O:	fio.h
rsfe.$O:	fmt.h
rsli.$O:	fio.h
rsli.$O:	lio.h
rsne.$O:	fio.h
rsne.$O:	lio.h
sfe.$O:		fio.h
sue.$O:		fio.h
uio.$O:		fio.h
util.$O:	fio.h
wref.$O:	fio.h
wref.$O:	fmt.h
wref.$O:	fp.h
wrtfmt.$O:	fio.h
wrtfmt.$O:	fmt.h
wsfe.$O:	fio.h
wsfe.$O:	fmt.h
wsle.$O:	fio.h
wsle.$O:	fmt.h
wsle.$O:	lio.h
wsne.$O:	fio.h
wsne.$O:	lio.h
xwsne.$O:	fio.h
xwsne.$O:	lio.h
xwsne.$O:	fmt.h

check:
	xsum -r Notice README Version.c backspace.c close.c dfe.c dolio.c \
	due.c endfile.c err.c f2ch.add fio.h fmt.c fmt.h fmtlib.c fp.h \
	iio.c ilnw.c inquire.c lio.h lread.c lwrite.c makefile open.c \
	rawio.h rdfmt.c rewind.c rsfe.c rsli.c rsne.c sfe.c sue.c \
	typesize.c uio.c util.c wref.c wrtfmt.c wsfe.c wsle.c wsne.c \
	xwsne.c >zap
	cmp zap libI77.xsum && rm zap || diff libI77.xsum zap
