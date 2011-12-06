noinst_LTLIBRARIES = libns.la

# if ARCH_ARM_HAVE_NEON
# nsx_core_neon.c
# endif

if NS_FIXED
libns_la_SOURCES = noise_suppression_x.c nsx_core.c
else
libns_la_SOURCES = noise_suppression.c ns_core.c
endif
libns_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
		  -I$(top_srcdir)/src/common_audio/signal_processing/include \
		  -I$(top_srcdir)/src/modules/audio_processing/utility \
		  -I$(top_srcdir)/src/system_wrappers/interface

