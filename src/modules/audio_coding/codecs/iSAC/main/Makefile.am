lib_LTLIBRARIES = libwebrtc_codecs_isac.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = interface/isac.h

libwebrtc_codecs_isac_la_SOURCES = \
				   source/arith_routines.c \
				   source/arith_routines_hist.c \
				   source/arith_routines_logist.c \
				   source/bandwidth_estimator.c \
				   source/crc.c \
				   source/decode.c \
				   source/decode_bwe.c \
				   source/encode.c \
				   source/encode_lpc_swb.c \
				   source/entropy_coding.c \
				   source/fft.c \
				   source/filter_functions.c \
				   source/filterbank_tables.c \
				   source/filterbanks.c \
				   source/intialize.c \
				   source/isac.c \
				   source/lattice.c \
				   source/lpc_analysis.c \
				   source/lpc_gain_swb_tables.c \
				   source/lpc_shape_swb12_tables.c \
				   source/lpc_shape_swb16_tables.c \
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
