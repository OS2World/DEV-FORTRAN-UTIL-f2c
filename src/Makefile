#	Makefile for f2c, a Fortran 77 to C converter

#g = -g
#CFLAGS = $g
#SHELL = /bin/sh
##############
# static libs
#AR = ar
#RANLIB = ar sv
#A = a
#O = o
#CFLAGS = -s -O2 -DOS2
##############
# dynamic libs
AR = emxomfar
RANLIB = emxomfar sv
A = lib
O = obj
CFLAGS = -Zomf -Zmtd -s -O2 -DOS2
##############
EXE = .exe
.SUFFIXES:
.SUFFIXES: $(EXE) .$A .$O .c .h
CC = gcc -ansi
ARFLAGS = rv
YACC = yacc
YFLAGS = -dv
##############
SHELL = ksh
SHELLFLAGS = -c
COMMAND = "$(CMNDNAME) $(CMNDARGS)"

.c.$O:
	$(CC) -c $(CFLAGS) $*.c
 

OBJECTSd = main.$O init.$O gram.$O lex.$O proc.$O equiv.$O data.$O format.$O \
	  expr.$O exec.$O intr.$O io.$O misc.$O error.$O mem.$O names.$O \
	  output.$O p1output.$O pread.$O put.$O putpcc.$O vax.$O formatdata.$O \
	  parse_args.$O niceprintf.$O cds.$O sysdep.$O version.$O
OBJECTS = $(OBJECTSd)

all: xsum.out f2c$(EXE)

f2c$(EXE): $(OBJECTS)
	$(CC) $(CFLAGS) $(LDFLAGS) f2c.def $(OBJECTS) -o f2c$(EXE)

gram.c:	gram.head gram.dcl gram.expr gram.exec gram.io defs.h tokdefs.h
	( sed <tokdefs.h 's/#define/%token/' ;\
		cat gram.head gram.dcl gram.expr gram.exec gram.io ) >gram.in
	$(YACC) $(YFLAGS) gram.in
	echo '(expect 4 shift/reduce)'
	sed 's/^# line.*/\/* & *\//' y.tab.c >gram.c
	rm -f gram.in y.tab.c

$(OBJECTSd): defs.h ftypes.h defines.h machdefs.h sysdep.h

tokdefs.h: tokens
	grep -n . <tokens | sed 's/\([^:]*\):\(.*\)/#define \2 \1/' >tokdefs.h

cds.$O: sysdep.h
exec.$O: p1defs.h names.h
expr.$O: output.h niceprintf.h names.h
format.$O: p1defs.h format.h output.h niceprintf.h names.h iob.h
formatdata.$O: format.h output.h niceprintf.h names.h
gram.$O: p1defs.h
init.$O: output.h niceprintf.h iob.h
intr.$O: names.h
io.$O: names.h iob.h
lex.$O : tokdefs.h p1defs.h
main.$O: parse.h usignal.h
mem.$O: iob.h
names.$O: iob.h names.h output.h niceprintf.h
niceprintf.$O: defs.h names.h output.h niceprintf.h
output.$O: output.h niceprintf.h names.h
p1output.$O: p1defs.h output.h niceprintf.h names.h
parse_args.$O: parse.h
proc.$O: tokdefs.h names.h niceprintf.h output.h p1defs.h
put.$O: names.h pccdefs.h p1defs.h
putpcc.$O: names.h
vax.$O: defs.h output.h pccdefs.h
output.h: niceprintf.h

put.$O putpcc.$O: pccdefs.h

f2c.t: f2c.1t
	troff -man f2c.1t >f2c.t

#f2c.1: f2c.1t
#	nroff -man f2c.1t | col -b | uniq >f2c.1

clean:
	rm -f gram.c *.$O f2c$(EXE) tokdefs.h f2c.t

b = Notice README cds.c data.c defines.h defs.h equiv.c error.c \
	exec.c expr.c f2c.1 f2c.1t f2c.h format.c format.h formatdata.c \
	ftypes.h gram.dcl gram.exec gram.expr gram.head gram.io \
	init.c intr.c io.c iob.h lex.c machdefs.h main.c \
	malloc.c mem.c memset.c misc.c names.c names.h niceprintf.c \
	niceprintf.h output.c output.h p1defs.h p1output.c \
	parse.h parse_args.c pccdefs.h pread.c proc.c put.c putpcc.c \
	sysdep.c sysdep.h tokens usignal.h vax.c version.c xsum.c

bundle:
	bundle $b makefile xsum0.out >/tmp/f2c.bundle

xsum$(EXE): xsum.c
	$(CC) $(CFLAGS) -o xsum$(EXE) xsum.c

#Check validity of transmitted source...
xsum.out: xsum$(EXE) $b
	xsum $b >xsum1.out
	cmp xsum0.out xsum1.out && mv xsum1.out xsum.out

#On non-Unix systems that end lines with carriage-return/newline pairs,
#use "make xsumr.out" rather than "make xsum.out".  The -r flag ignores
#carriage-return characters.
xsumr.out: xsum$(EXE) $b
	xsum -r $b >xsum1.out
	cmp xsum0.out xsum1.out && mv xsum1.out xsumr.out
