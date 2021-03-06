#
# crypto/camellia/Makefile
#

DIR= camellia
TOP=	../..
CC=	cc
CPP=	$(CC) -E
INCLUDES=
CFLAG=-g
MAKEFILE=	Makefile
AR=		ar r

CMLL_ENC= camellia.o cmll_misc.o cmll_cbc.o

CFLAGS= $(INCLUDES) $(CFLAG)
ASFLAGS= $(INCLUDES) $(ASFLAG)
AFLAGS= $(ASFLAGS)

GENERAL=Makefile

LIB=$(TOP)/libcrypto.a
LIBSRC=camellia.c cmll_misc.c cmll_ecb.c cmll_cbc.c cmll_ofb.c \
	   cmll_cfb.c cmll_ctr.c 

LIBOBJ= cmll_ecb.o cmll_ofb.o cmll_cfb.o cmll_ctr.o $(CMLL_ENC)

SRC= $(LIBSRC)

HEADER= cmll_locl.h

ALL=    $(GENERAL) $(SRC) $(HEADER)

top:
	(cd ../..; $(MAKE) DIRS=crypto SDIRS=$(DIR) sub_all)

all:	lib

lib:	$(LIBOBJ)
	$(AR) $(LIB) $(LIBOBJ)
	$(RANLIB) $(LIB) || echo Never mind.
	@touch lib

cmll-x86.s:	asm/cmll-x86.pl ../perlasm/x86asm.pl
	$(PERL) asm/cmll-x86.pl $(PERLASM_SCHEME) $(CFLAGS) $(PROCESSOR) > $@
cmll-x86_64.s:  asm/cmll-x86_64.pl
	$(PERL) asm/cmll-x86_64.pl $(PERLASM_SCHEME) > $@
cmllt4-sparcv9.s: asm/cmllt4-sparcv9.pl ../perlasm/sparcv9_modes.pl
	$(PERL) asm/cmllt4-sparcv9.pl $(CFLAGS) > $@

files:
	$(PERL) $(TOP)/util/files.pl Makefile >> $(TOP)/MINFO

tags:
	ctags $(SRC)

tests:

lint:
	lint -DLINT $(INCLUDES) $(SRC)>fluff

depend:
	@[ -n "$(MAKEDEPEND)" ] # should be set by upper Makefile...
	$(MAKEDEPEND) -- $(CFLAG) $(INCLUDES) $(DEPFLAG) -- $(PROGS) $(LIBSRC)

dclean:
	$(PERL) -pe 'if (/^# DO NOT DELETE THIS LINE/) {print; exit(0);}' $(MAKEFILE) >Makefile.new
	mv -f Makefile.new $(MAKEFILE)

clean:
	rm -f *.s *.o *.obj lib tags core .pure .nfs* *.old *.bak fluff

# DO NOT DELETE THIS LINE -- make depend depends on it.

camellia.o: ../../include/openssl/camellia.h
camellia.o: ../../include/openssl/opensslconf.h camellia.c cmll_locl.h
cmll_cbc.o: ../../include/openssl/camellia.h ../../include/openssl/modes.h
cmll_cbc.o: ../../include/openssl/opensslconf.h cmll_cbc.c
cmll_cfb.o: ../../include/openssl/camellia.h ../../include/openssl/modes.h
cmll_cfb.o: ../../include/openssl/opensslconf.h cmll_cfb.c
cmll_ctr.o: ../../include/openssl/camellia.h ../../include/openssl/modes.h
cmll_ctr.o: ../../include/openssl/opensslconf.h cmll_ctr.c
cmll_ecb.o: ../../include/openssl/camellia.h
cmll_ecb.o: ../../include/openssl/opensslconf.h cmll_ecb.c cmll_locl.h
cmll_misc.o: ../../include/openssl/camellia.h
cmll_misc.o: ../../include/openssl/opensslconf.h
cmll_misc.o: ../../include/openssl/opensslv.h cmll_locl.h cmll_misc.c
cmll_ofb.o: ../../include/openssl/camellia.h ../../include/openssl/modes.h
cmll_ofb.o: ../../include/openssl/opensslconf.h cmll_ofb.c
