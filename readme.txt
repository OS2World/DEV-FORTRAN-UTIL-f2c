
====== old index for f2c, now "readme from f2c" ============

FILES:

f2c.h	Include file necessary for compiling output of the converter.
	See the second NOTE below.

f2c.1	Man page for f2c.

f2c.1t	Source for f2c.1 (to be processed by troff -man or nroff -man).

libf77	Library of non I/O support routines the generated C may need.
	Fortran main programs result in a C function named MAIN__ that
	is meant to be invoked by the main() in libf77.

libi77	Library of Fortran I/O routines the generated C may need.
	Note that some vendors (e.g., BSD, Sun and MIPS) provide a
	libF77 and libI77 that are incompatible with f2c -- they
	provide some differently named routines or routines with the
	names that f2c expects, but with different calling sequences.
	On such systems, the recommended procedure is to merge
	libf77 and libi77 into a single library, say libf2c, and to
        install it where you can access it by specifying -lf2c .  The
        definition of link_msg in sysdep.c assumes this arrangement.

f2c.ps	Postscript for a technical report on f2c.  After you strip the
	mail header, the first line should be "%!PS".

fixes	The complete change log, reporting bug fixes and other changes.
	(Some recent change-log entries are given below).

fc	A shell script that uses f2c and imitates much of the behavior
	of commonly found f77 commands.  You will almost certainly
	need to adjust some of the shell-variable assignments to make
	this script work on your system.


SUBDIRECTORY:

f2c/src	Source for the converter itself, including a file of checksums
	and source for a program to compute the checksums (to verify
	correct transmission of the source), is available: ask netlib to
		send all from f2c/src
	If the checksums show damage to just a few source files, or if
	the change log file (see "fixes" below) reports corrections to
	some source files, you can request those files individually
	"from f2c/src".  For example, to get defs.h and xsum0.out, you
	would ask netlib to
		send defs.h xsum0.out from f2c/src
	"all from f2c/src" is about 640 kilobytes long; for convenience
	(and checksums), it includes copies of f2c.h, f2c.1, and f2c.1t.

	Tip: if asked to send over 99,000 bytes in one request, netlib
	breaks the shipment into 1000 line pieces and sends each piece
	separately (since otherwise some mailers might gag).  To avoid
	the hassle of reassembling the pieces, try to keep each request
	under 99,000 bytes long.  The final number in each line of
	xsum0.out gives the length of each file in f2c/src.  For
	example,
		send exec.c expr.c from f2c/src
		send format.c format_data.c from f2c/src
	will give you slightly less hassle than
		send exec.c expr.c format.c format_data.c from f2c/src
	Alternatively, if all the mailers in your return path allow
	long messages, you can supply an appropriate mailsize line in
	your netlib request, e.g.
		mailsize 200k
		send exec.c expr.c format.c format_data.c from f2c/src

	If you have trouble generating gram.c, you can ask netlib to
		send gram.c from f2c/src
	Then `xsum gram.c` should report
		gram.c	1814e302	57355

NOTE:	For now, you may exercise f2c by sending netlib a message whose
	first line is "execute f2c" and whose remaining lines are
	the Fortran 77 source that you wish to have converted.
	Return mail brings you the resulting C, with f2c's error
	messages between #ifdef uNdEfInEd and #endif at the end.
	(To understand line numbers in the error messages, regard
	the "execute f2c" line as line 0.  It is stripped away by
	the netlib software before f2c sees your Fortran input.)
	Options described in the man page may be transmitted to
	netlib by having the first line of input be a comment
	whose first 6 characters are "c$f2c " and whose remaining
	characters are the desired options, e.g., "c$f2c -R -u".
	This scheme may change -- ask netlib to
               send index from f2c
        if you do not get the behavior you expect.

	During the initial experimental period, incoming Fortran
	will be saved in a file.  Don't send any secrets!


BUGS:	Please send bug reports (including the shortest example
	you can find that illustrates the bug) to research!dmg
	or dmg@research.att.com .  You might first check whether
	the bug goes away when you turn optimization off.


NOTE:	f2c.h defines several types, e.g., real, integer, doublereal.
	The definitions in f2c.h are suitable for most machines, but if
	your machine has sizeof(double) > 2*sizeof(long), you may need
	to adjust f2c.h appropriately.  f2c assumes
		sizeof(doublecomplex) = 2*sizeof(doublereal)
		sizeof(doublereal) = sizeof(complex)
		sizeof(doublereal) = 2*sizeof(real)
		sizeof(real) = sizeof(integer)
		sizeof(real) = sizeof(logical)
		sizeof(real) = 2*sizeof(shortint)
	EQUIVALENCEs may not be translated correctly if these
	assumptions are violated.

	There exists a C compiler that objects to the lines
		typedef VOID C_f;	/* complex function */
		typedef VOID H_f;	/* character function */
		typedef VOID Z_f;	/* double complex function */
	in f2c.h .  If yours is such a compiler, do two things:
	1. Complain to your vendor about this compiler bug.
	2. Find the line
		#define VOID void
	   in f2c.h and change it to
		#define VOID int
	(For readability, the f2c.h lines shown above have had two
	tabs inserted before their first character.)

FTP:	All the material described above is now available by anonymous
	ftp from netlib.att.com (login: anonymous; Password: your E-mail
	address; cd netlib/f2c).  Note that you can say, e.g.,

		cd /netlib/f2c/src
		binary
		prompt
		mget *.Z

	to get all the .Z files in src.  You must uncompress the .Z
	files once you have a copy of them, e.g., by

		uncompress *.Z

	Subdirectory msdos contains two PC versions of f2c,
	f2c.exe.Z and f2cx.exe.Z; the latter uses extended memory.
	The README in that directory provides more details.

-----------------
Recent change log (partial)
-----------------

Tue May 10 07:55:12 EDT 1994
  Trivial changes to exec.c, p1output.c, parse_args.c, proc.c,
and putpcc.c: change arguments from
	type foo[]
to
	type *foo
for consistency with defs.h.  For most compilers, this makes no
difference.

Thu Jun  2 12:18:18 EDT 1994
  Fix bug in handling FORMAT statements that have adjacent character
(or Hollerith) strings: an extraneous \002 appeared between the
strings.
  libf77: under -DNO_ONEXIT, arrange for f_exit to be called just
once; previously, upon abnormal termination (including stop statements),
it was called twice.

Mon Jun  6 15:52:57 EDT 1994
  libf77: Avoid references to SIGABRT and SIGIOT if neither is defined;
Version.c not changed.
  libi77: Add cast to definition of errfl() in fio.h; this only matters
on systems with sizeof(int) < sizeof(long).  Under -DNON_UNIX_STDIO,
use binary mode for direct formatted files (to avoid any confusion
connected with \n characters).

Fri Jun 10 16:47:31 EDT 1994
  Fix bug under -A in handling unreferenced (and undeclared)
external arguments in subroutines with multiple entry points.  Example:
	subroutine m(fcn,futil)
	external fcn,futil
	call fcn
	entry mintio(i1) ! (D_fp)0 rather than (U_fp)0 for futil
	end

Wed Jun 15 10:38:14 EDT 1994
  Allow char(constant expression) function in parameter declarations.
(This was probably broken in the changes of 29 March 1994.)

Fri Jul  1 23:54:00 EDT 1994
  Minor adjustments to makefile (rule for f2c.1 commented out) and
sysdep.h (#undef KR_headers if __STDC__ is #defined, and base test
for ANSI_Libraries and ANSI_Prototypes on KR_headers rather than
__STDC__); version.c touched but not changed.
  libi77: adjust fp.h so local.h is only needed under -DV10.

Tue Jul  5 03:05:46 EDT 1994
  Fix segmentation fault in
	subroutine foo(a,b,k)
	data i/1/
	double precision a(k,1)	! sequence error: must precede data
	b = a(i,1)
	end
  libi77: Fix bug (introduced 6 June 1994?) in reopening files under
NON_UNIX_STDIO.
  Fix some error messages caused by illegal Fortran.  Examples:
* 1.
	x(i) = 0  !Missing declaration for array x
	call f(x) !Said Impossible storage class 8 in routine mkaddr
	end	  !Now says invalid use of statement function x
* 2.
	f = g	!No declaration for g; by default it's a real variable
	call g	!Said invalid class code 2 for function g
	end	!Now says g cannot be called
* 3.
	intrinsic foo	!Invalid intrinsic name
	a = foo(b)	!Said intrcall: bad intrgroup 0
	end		!Now just complains about line 1

Tue Jul  5 11:14:26 EDT 1994
  Fix glitch in handling erroneous statement function declarations.
Example:
	a(j(i) - i) = a(j(i) - i) + 1	! bad statement function
	call foo(a(3))	! Said Impossible type 0 in routine mktmpn
	end		! Now warns that i and j are not used

Wed Jul  6 17:31:25 EDT 1994
  Tweak test for statement functions that (illegally) call themselves;
f2c will now proceed to check for other errors, rather than bailing
out at the first recursive statement function reference.
  Warn about but retain divisions by 0 (instead of calling them
"compiler errors" and quiting).  On IEEE machines, this permits
	double precision nan, ninf, pinf
	nan = 0.d0/0.d0
	pinf = 1.d0/0.d0
	ninf = -1.d0/0.d0
	write(*,*) 'nan, pinf, ninf = ', nan, pinf, ninf
	end
to print
	nan, pinf, ninf =   NaN  Infinity -Infinity
  libi77: wref.c: protect with #ifdef GOOD_SPRINTF_EXPONENT an
optimization that requires exponents to have 2 digits when 2 digits
suffice.  lwrite.c wsfe.c (list and formatted external output):
omit ' ' carriage-control when compiled with -DOMIT_BLANK_CC .
Off-by-one bug fixed in character count for list output of character
strings.  Omit '.' in list-directed printing of Nan, Infinity.

Mon Jul 11 13:05:33 EDT 1994
  src/gram.c updated.

Tue Jul 12 10:24:42 EDT 1994
  libi77: wrtfmt.c: under G11.4, write 0. as "  .0000    " rather
than "  .0000E+00".

Thu Jul 14 17:55:46 EDT 1994
  Fix glitch in changes of 6 July 1994 that could cause erroneous
"division by zero" warnings (or worse).  Example:
	subroutine foo(a,b)
	y = b
	a = a / y	! erroneous warning of division by zero
	end

Current timestamps of files in "all from f2c/src", sorted by time,
appear below (mm/dd/year hh:mm:ss).  To bring your source up to date,
obtain source files with a timestamp later than the time shown in your
version.c.  Note that the time shown in the current version.c is the
timestamp of the source module that immediately follows version.c below:

 7/14/1994  17:55:17  xsum0.out
 7/14/1994  17:54:58  version.c
 7/14/1994  17:54:51  expr.c
 7/06/1994  15:47:09  exec.c
 7/06/1994   9:33:19  defs.h
 7/05/1994   1:02:52  proc.c
 7/05/1994   0:54:42  output.c
 7/04/1994  23:56:08  vax.c
 7/01/1994  23:46:42  sysdep.h
 7/01/1994  23:24:55  makefile
 6/15/1994  10:34:02  data.c
 6/01/1994  11:04:14  io.c
 5/10/1994   7:42:54  putpcc.c
 5/10/1994   7:42:53  parse_args.c
 5/10/1994   7:42:53  p1output.c
 3/05/1994   2:02:49  f2c.1
 3/05/1994   2:02:42  f2c.1t
 3/05/1994   1:05:18  main.c
 3/05/1994   0:57:28  sysdep.c
 3/05/1994   0:56:34  names.c
 3/04/1994  23:58:15  misc.c
 3/04/1994  23:42:15  pread.c
 2/28/1994  11:32:36  README
 2/25/1994  22:18:14  xsum.c
 2/25/1994  14:16:00  Notice
 2/25/1994  12:18:21  format.c
 2/25/1994  12:18:21  lex.c
 2/25/1994  11:01:20  niceprintf.c
 2/25/1994  10:56:33  error.c
 2/25/1994  10:25:21  gram.head
 2/25/1994  10:24:56  put.c
 2/25/1994  10:24:54  init.c
 2/25/1994  10:24:54  mem.c
 2/25/1994  10:24:54  formatdata.c
 2/25/1994  10:24:54  malloc.c
 2/25/1994  10:24:54  intr.c
 2/25/1994  10:24:53  equiv.c
 2/25/1994  10:24:52  cds.c
 2/25/1994   2:07:19  parse.h
 2/22/1994  19:07:20  iob.h
 2/22/1994  18:56:53  p1defs.h
 2/22/1994  18:53:46  output.h
 2/22/1994  18:51:14  names.h
 2/22/1994  18:30:41  format.h
 1/18/1994  18:12:52  tokens
 1/18/1994  18:12:52  gram.dcl
 6/01/1993  23:10:00  f2c.h
 3/06/1993  14:13:58  gram.expr
 3/04/1993  14:59:25  gram.exec
 1/28/1993   9:03:16  ftypes.h
 1/25/1993  11:26:33  defines.h
 4/06/1990   0:00:57  gram.io
 2/03/1990   0:58:26  niceprintf.h
 1/29/1990  13:26:52  memset.c
 1/07/1990   1:20:01  usignal.h
11/27/1989   8:27:37  machdefs.h
 7/01/1989  11:59:44  pccdefs.h
