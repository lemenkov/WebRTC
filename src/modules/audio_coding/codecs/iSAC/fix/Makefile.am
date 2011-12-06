lib_LTLIBRARIES = libwebrtc_codecs_isac.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = interface/isacfix.h

# Android-specific
# if ARCH_ARM_HAVE_ARMV7A
# fix/source/lattice_armv7.S
# fix/source/pitchfilter_armv6.S
#
# if WEBRTC_BUILD_NEON_LIBS
# fix/source/filters_neon.c
# fix/source/lattice_neon.S

libwebrtc_codecs_isac_la_SOURCES = \
				   source/arith_routines.c \
				   source/arith_routines_hist.c \
				   source/arith_routines_logist.c \
				   source/bandwidth_estimator.c \
				   source/decode.c \
				   source/decode_bwe.c \
				   source/decode_plc.c \
				   source/encode.c \
				   source/entropy_coding.c \
				   source/fft.c \
				   source/filterbank_tables.c \
				   source/filterbanks.c \
				   source/filters.c \
				   source/initialize.c \
				   source/isacfix.c \
				   source/lattice.c \
				   source/lattice_c.c \
				   source/lpc_masking_model.c \
				   source/lpc_tables.c \
				   source/pitch_estimator.c \
				   source/pitch_filter.c \
				   source/pitch_gain_tables.c \
				   source/pitch_lag_tables.c \
				   source/spectrum_ar_model_tables.c \
				   source/transform.c


libwebrtc_codecs_isac_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
			-I$(top_srcdir)/src/common_audio/signal_processing/include

libwebrtc_codecs_isac_la_LIBADD = $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la

libwebrtc_codecs_isac_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)
