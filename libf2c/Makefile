##############
# static libs
#AR = ar
#RANLIB = ar sv
#A = a
#O = o
##############
# dynamic libs
AR = emxomfar
RANLIB = emxomfar sv
A = lib
O = obj
##############
.SUFFIXES:
.SUFFIXES: .exe .$A .$O .c .h
ARFLAGS = rv
CC = gcc -ansi -I..
SHELL = ksh
SHELLFLAGS = -c
COMMAND = "$(CMNDNAME) $(CMNDARGS)"

F2COBJS= \
	abort_.$O backspace.$O c_abs.$O c_cos.$O c_div.$O c_exp.$O \
	c_log.$O c_sin.$O c_sqrt.$O cabs.$O close.$O d_abs.$O \
	d_acos.$O d_asin.$O d_atan.$O d_atn2.$O d_cnjg.$O d_cos.$O \
	d_cosh.$O d_dim.$O d_exp.$O d_imag.$O d_int.$O d_lg10.$O \
	d_log.$O d_mod.$O d_nint.$O d_prod.$O d_sign.$O d_sin.$O \
	d_sinh.$O d_sqrt.$O d_tan.$O d_tanh.$O derf_.$O derfc_.$O \
	dfe.$O dolio.$O due.$O ef1asc_.$O ef1cmc_.$O endfile.$O \
	erf_.$O erfc_.$O err.$O fmt.$O fmtlib.$O getarg_.$O \
	getenv_.$O h_abs.$O h_dim.$O h_dnnt.$O h_indx.$O h_len.$O \
	h_mod.$O h_nint.$O h_sign.$O hl_ge.$O hl_gt.$O hl_le.$O \
	hl_lt.$O i_abs.$O i_dim.$O i_dnnt.$O i_indx.$O i_len.$O \
	i_mod.$O i_nint.$O i_sign.$O iargc_.$O iio.$O ilnw.$O \
	inquire.$O l_ge.$O l_gt.$O l_le.$O l_lt.$O lread.$O \
	lwrite.$O main.$O open.$O pow_ci.$O pow_dd.$O pow_di.$O \
	pow_hh.$O pow_ii.$O pow_ri.$O pow_zi.$O pow_zz.$O r_abs.$O \
	r_acos.$O r_asin.$O r_atan.$O r_atn2.$O r_cnjg.$O r_cos.$O \
	r_cosh.$O r_dim.$O r_exp.$O r_imag.$O r_int.$O r_lg10.$O \
	r_log.$O r_mod.$O r_nint.$O r_sign.$O r_sin.$O r_sinh.$O \
	r_sqrt.$O r_tan.$O r_tanh.$O rdfmt.$O rewind.$O rsfe.$O \
	rsli.$O rsne.$O s_cat.$O s_cmp.$O s_copy.$O s_paus.$O \
	s_rnge.$O s_stop.$O sfe.$O sig_die.$O signal_.$O sue.$O \
	system_.$O typesize.$O uio.$O util.$O wref.$O wrtfmt.$O \
	wsfe.$O wsle.$O wsne.$O xwsne.$O z_abs.$O z_cos.$O \
	z_div.$O z_exp.$O z_log.$O z_sin.$O z_sqrt.$O

f2c.$A : $(F2COBJS)
	$(AR) $(ARFLAGS) f2c.$A $?
	$(RANLIB) f2c.$A

F2CLIBOBJS= \
	derf_.$O derfc_.$O erf_.$O erfc_.$O getarg_.$O iargc_.$O main.$O

f2clib.$A : $(F2CLIBOBJS)
	$(AR) $(ARFLAGS) f2clib.$A $?
	$(RANLIB) f2clib.$A

F2CDLLOBJS= \
	abort_.$O backspace.$O c_abs.$O c_cos.$O c_div.$O c_exp.$O \
	c_log.$O c_sin.$O c_sqrt.$O cabs.$O close.$O d_abs.$O d_acos.$O \
	d_asin.$O d_atan.$O d_atn2.$O d_cnjg.$O d_cos.$O d_cosh.$O \
	d_dim.$O d_exp.$O d_imag.$O d_int.$O d_lg10.$O d_log.$O \
	d_mod.$O d_nint.$O d_prod.$O d_sign.$O d_sin.$O d_sinh.$O \
	d_sqrt.$O d_tan.$O d_tanh.$O dfe.$O dolio.$O due.$O ef1asc_.$O \
	ef1cmc_.$O endfile.$O err.$O fmt.$O fmtlib.$O getenv_.$O \
	h_abs.$O h_dim.$O h_dnnt.$O h_indx.$O h_len.$O h_mod.$O \
	h_nint.$O h_sign.$O hl_ge.$O hl_gt.$O hl_le.$O hl_lt.$O \
	i_abs.$O i_dim.$O i_dnnt.$O i_indx.$O i_len.$O i_mod.$O \
	i_nint.$O i_sign.$O iio.$O ilnw.$O inquire.$O l_ge.$O l_gt.$O \
	l_le.$O l_lt.$O lread.$O lwrite.$O open.$O pow_ci.$O pow_dd.$O \
	pow_di.$O pow_hh.$O pow_ii.$O pow_ri.$O pow_zi.$O pow_zz.$O \
	r_abs.$O r_acos.$O r_asin.$O r_atan.$O r_atn2.$O r_cnjg.$O \
	r_cos.$O r_cosh.$O r_dim.$O r_exp.$O r_imag.$O r_int.$O \
	r_lg10.$O r_log.$O r_mod.$O r_nint.$O r_sign.$O r_sin.$O \
	r_sinh.$O r_sqrt.$O r_tan.$O r_tanh.$O rdfmt.$O rewind.$O \
	rsfe.$O rsli.$O rsne.$O s_cat.$O s_cmp.$O s_copy.$O s_paus.$O \
	s_rnge.$O s_stop.$O sfe.$O sig_die.$O signal_.$O sue.$O \
	system_.$O typesize.$O uio.$O util.$O wref.$O wrtfmt.$O \
	wsfe.$O wsle.$O wsne.$O xwsne.$O z_abs.$O z_cos.$O z_div.$O \
	z_exp.$O z_log.$O z_sin.$O z_sqrt.$O

# target for import library

f2cdll.$A: f2cdll.def
	emximp -o f2cdll.$A f2cdll.def

# target for dll library

f2cdll.dll: dllobj.$A f2cdll.def
	$(CC) -o f2cdll.dll dllobj.$A f2cdll.def -Zdll -Zomf -Zmtd -mprobe

dllobj.$A : $(F2CDLLOBJS)
	$(AR) $(ARFLAGS) dllobj.$A $?
	$(RANLIB) dllobj.$A

f2cdll.def: f2cdll.df dllobj.$A
	copy f2cdll.df f2cdll.def
	emxexp dllobj.$A >>f2cdll.def

