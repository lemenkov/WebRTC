noinst_LTLIBRARIES = libagc.la

libagc_la_SOURCES = analog_agc.c \
		    digital_agc.c
libagc_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
		   -I$(top_srcdir)/src/common_audio/signal_processing/include \
		   -I$(top_srcdir)/src/modules/audio_processing/utility
