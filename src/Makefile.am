SUBDIRS	= jansson-2.10

ACLOCAL_AMFLAGS = -I m4
AM_CPPFLAGS =  -I$(top_srcdir)/src/jansson-2.10/src

native_objs :=

if HAVE_AVX2
native_objs += sha256_code_release/sha256_avx2_rorx2.A
endif
if HAVE_AVX1
native_objs += sha256_code_release/sha256_avx1.A
endif
if HAVE_SSE4
native_objs += sha256_code_release/sha256_sse4.A
endif

%.A: %.asm
	yasm -f x64 -f elf64 -X gnu -g dwarf2 -D LINUX -o $@ $<

noinst_LIBRARIES = libckpool.a
libckpool_a_SOURCES = libckpool.c libckpool.h sha2.c sha2.h \
  crypto/w_blake.c \
  crypto/w_bmw.c \
  crypto/w_cubehash.c \
  crypto/w_echo.c \
  crypto/w_fugue.c \
  crypto/w_groestl.c \
  crypto/w_hamsi.c \
  crypto/w_aes_helper.c \
  crypto/w_jh.c \
  crypto/w_keccak.c \
  crypto/w_luffa.c \
  crypto/w_shavite.c \
  crypto/w_simd.c \
  crypto/w_sha2big.c \
  crypto/w_haval.c \
  crypto/w_panama.c \
  crypto/w_blake256.c \
  crypto/w_skein256.c \
  crypto/w_shabal.c \
  crypto/w_skein.c \
  crypto/w_blake.h \
  crypto/w_bmw.h \
  crypto/w_cubehash.h \
  crypto/w_echo.h \
  crypto/w_fugue.h \
  crypto/w_groestl.h \
  crypto/w_hamsi.h \
  crypto/w_hamsi_helper.h \
  crypto/w_jh.h \
  crypto/w_keccak.h \
  crypto/w_luffa.h \
  crypto/w_shavite.h \
  crypto/w_simd.h \
  crypto/w_sha2big.h \
  crypto/w_haval.h \
  crypto/w_panama.h \
  crypto/w_blake256.h \
  crypto/w_skein256.h \
  crypto/w_shabal.h \
  crypto/w_skein.h
libckpool_a_LIBADD = $(native_objs)

bin_PROGRAMS = ckpool ckpmsg notifier
ckpool_SOURCES = ckpool.c ckpool.h generator.c generator.h bitcoin.c bitcoin.h \
		 stratifier.c stratifier.h connector.c connector.h uthash.h \
		 utlist.h
ckpool_LDADD = libckpool.a @JANSSON_LIBS@ @LIBS@

ckpmsg_SOURCES = ckpmsg.c
ckpmsg_LDADD = libckpool.a @JANSSON_LIBS@

notifier_SOURCES = notifier.c
notifier_LDADD = libckpool.a @JANSSON_LIBS@

if WANT_CKDB
bin_PROGRAMS += ckdb
ckdb_SOURCES = ckdb.c ckdb_cmd.c ckdb_data.c ckdb_dbio.c ckdb_btc.c \
		ckdb_crypt.c ckdb.h klist.c ktree.c klist.h ktree.h
ckdb_LDADD = libckpool.a @JANSSON_LIBS@ @LIBS@
endif
