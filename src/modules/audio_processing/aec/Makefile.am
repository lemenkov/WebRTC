noinst_LTLIBRARIES = libaec.la

if WITH_SSE2
sse2_SOURCES = aec_core_sse2.c aec_rdft_sse2.c
else
sse2_SOURCES =
endif

#DEFS += -DWEBRTC_AEC_DEBUG_DUMP

libaec_la_SOURCES = \
		    aec_core.c \
		    aec_rdft.c \
		    aec_resampler.c \
		    echo_cancellation.c \
		    $(sse2_SOURCES)

libaec_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
		   -I$(top_srcdir)/src/common_audio/signal_processing/include \
		   -I$(top_srcdir)/src/system_wrappers/interface \
		   -I$(top_srcdir)/src/modules/audio_processing/utility
