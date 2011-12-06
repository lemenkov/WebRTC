noinst_LTLIBRARIES = libaecm.la

# if ARCH_ARM_HAVE_NEON
# aecm_core_neon.c
# aecm_core_neon.S
# aecm_core_neon_offsets.c
# fi

libaecm_la_SOURCES = aecm_core.c echo_control_mobile.c

libaecm_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
		    -I$(top_srcdir)/src/common_audio/signal_processing/include \
		    -I$(top_srcdir)/src/system_wrappers/interface \
		    -I$(top_srcdir)/src/modules/audio_processing/utility
