noinst_LTLIBRARIES = libapm_util.la

libapm_util_la_SOURCES = delay_estimator.c \
			 delay_estimator_wrapper.c \
			 fft4g.c \
			 ring_buffer.c
libapm_util_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
			-I$(top_srcdir)/src/common_audio/signal_processing/include
