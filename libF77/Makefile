#.SUFFIXES: .c .o
#CC = cc
#SHELL = /bin/sh
#CFLAGS = -O

##############
# static libs
#AR = ar
#RANLIB = ar sv
#A = a
#O = o
#CFLAGS = -s -O -DOS2
##############
# dynamic libs
AR = emxomfar
RANLIB = emxomfar sv
A = lib
O = obj
CFLAGS = -Zomf -Zmtd -s -O -DOS2
#CFLAGS = -Zdll -Zomf -Zmtd -mprobe -s -O -DOS2 	# for DLL
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
 
# If your system lacks onexit() and you are not using an
# ANSI C compiler, then you should add -DNO_ONEXIT to CFLAGS,
# e.g., by changing the above "CFLAGS =" line to
# CFLAGS = -O -DNO_ONEXIT

# On at least some Sun systems, it is more appropriate to change the
# "CFLAGS =" line to
# CFLAGS = -O -Donexit=on_exit

# compile, then strip unnecessary symbols
#.c.o:
#	$(CC) -c -DSkip_f2c_Undefs $(CFLAGS) $*.c
#	ld -r -x -o $*.xxx $*.o
#	mv $*.xxx $*.o

MISC =	Version.$O main.$O s_rnge.$O abort_.$O getarg_.$O iargc_.$O getenv_.$O\
	signal_.$O s_stop.$O s_paus.$O system_.$O cabs.$O\
	derf_.$O derfc_.$O erf_.$O erfc_.$O sig_die.$O
POW =	pow_ci.$O pow_dd.$O pow_di.$O pow_hh.$O pow_ii.$O \
	pow_ri.$O pow_zi.$O pow_zz.$O
CX =	c_abs.$O c_cos.$O c_div.$O c_exp.$O c_log.$O c_sin.$O c_sqrt.$O
DCX =	z_abs.$O z_cos.$O z_div.$O z_exp.$O z_log.$O z_sin.$O z_sqrt.$O
REAL =	r_abs.$O r_acos.$O r_asin.$O r_atan.$O r_atn2.$O r_cnjg.$O r_cos.$O\
	r_cosh.$O r_dim.$O r_exp.$O r_imag.$O r_int.$O\
	r_lg10.$O r_log.$O r_mod.$O r_nint.$O r_sign.$O\
	r_sin.$O r_sinh.$O r_sqrt.$O r_tan.$O r_tanh.$O
DBL =	d_abs.$O d_acos.$O d_asin.$O d_atan.$O d_atn2.$O\
	d_cnjg.$O d_cos.$O d_cosh.$O d_dim.$O d_exp.$O\
	d_imag.$O d_int.$O d_lg10.$O d_log.$O d_mod.$O\
	d_nint.$O d_prod.$O d_sign.$O d_sin.$O d_sinh.$O\
	d_sqrt.$O d_tan.$O d_tanh.$O
INT =	i_abs.$O i_dim.$O i_dnnt.$O i_indx.$O i_len.$O i_mod.$O \
	i_nint.$O i_sign.$O
HALF =	h_abs.$O h_dim.$O h_dnnt.$O h_indx.$O h_len.$O h_mod.$O \
	h_nint.$O h_sign.$O
CMP =	l_ge.$O l_gt.$O l_le.$O l_lt.$O hl_ge.$O hl_gt.$O hl_le.$O hl_lt.$O
EFL =	ef1asc_.$O ef1cmc_.$O
CHAR =	s_cat.$O s_cmp.$O s_copy.$O

libF77.$A : $(MISC) $(POW) $(CX) $(DCX) $(REAL) $(DBL) $(INT) \
	$(HALF) $(CMP) $(EFL) $(CHAR)
	$(AR) $(ARFLAGS) libF77.$A $?
	$(RANLIB) libF77.$A

#Version.$O: Version.c
#	$(CC) -c Version.c

# To compile with C++, first "make f2c.h"
f2c.h: f2ch.add
	cat /usr/include/f2c.h f2ch.add >f2c.h

install:	libF77.$A
	mv libF77.$A /usr/lib

clean:
	rm -f libF77.$A *.$O

check:
	xsum -r Notice README Version.c abort_.c c_abs.c c_cos.c c_div.c \
	c_exp.c c_log.c c_sin.c c_sqrt.c cabs.c d_abs.c d_acos.c \
	d_asin.c d_atan.c d_atn2.c d_cnjg.c d_cos.c d_cosh.c d_dim.c \
	d_exp.c d_imag.c d_int.c d_lg10.c d_log.c d_mod.c d_nint.c \
	d_prod.c d_sign.c d_sin.c d_sinh.c d_sqrt.c d_tan.c d_tanh.c \
	derf_.c derfc_.c ef1asc_.c ef1cmc_.c erf_.c erfc_.c f2ch.add \
	getarg_.c getenv_.c h_abs.c h_dim.c h_dnnt.c h_indx.c h_len.c \
	h_mod.c h_nint.c h_sign.c hl_ge.c hl_gt.c hl_le.c hl_lt.c \
	i_abs.c i_dim.c i_dnnt.c i_indx.c i_len.c i_mod.c i_nint.c \
	i_sign.c iargc_.c l_ge.c l_gt.c l_le.c l_lt.c main.c makefile \
	pow_ci.c pow_dd.c pow_di.c pow_hh.c pow_ii.c pow_qq.c pow_ri.c \
	pow_zi.c pow_zz.c r_abs.c r_acos.c r_asin.c r_atan.c r_atn2.c \
	r_cnjg.c r_cos.c r_cosh.c r_dim.c r_exp.c r_imag.c r_int.c r_lg10.c \
	r_log.c r_mod.c r_nint.c r_sign.c r_sin.c r_sinh.c r_sqrt.c \
	r_tan.c r_tanh.c s_cat.c s_cmp.c s_copy.c s_paus.c s_rnge.c \
	s_stop.c sig_die.c signal_.c system_.c z_abs.c z_cos.c z_div.c \
	z_exp.c z_log.c z_sin.c z_sqrt.c >zap
	cmp zap libF77.xsum && rm zap || diff libF77.xsum zap
