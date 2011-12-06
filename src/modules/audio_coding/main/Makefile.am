lib_LTLIBRARIES = libwebrtc_audio_coding.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/audio_coding_module.h ./interface/audio_coding_module_typedefs.h

libwebrtc_audio_coding_la_SOURCES = \
				    source/acm_amr.cc \
				    source/acm_amrwb.cc \
				    source/acm_cng.cc \
				    source/acm_celt.cc \
				    source/acm_codec_database.cc \
				    source/acm_dtmf_detection.cc \
				    source/acm_dtmf_playout.cc \
				    source/acm_g722.cc \
				    source/acm_g7221.cc \
				    source/acm_g7221c.cc \
				    source/acm_g729.cc \
				    source/acm_g7291.cc \
				    source/acm_generic_codec.cc \
				    source/acm_gsmfr.cc \
				    source/acm_ilbc.cc \
				    source/acm_isac.cc \
				    source/acm_neteq.cc \
				    source/acm_opus.cc \
				    source/acm_pcm16b.cc \
				    source/acm_pcma.cc \
				    source/acm_pcmu.cc \
				    source/acm_red.cc \
				    source/acm_resampler.cc \
				    source/acm_speex.cc \
				    source/audio_coding_module.cc \
				    source/audio_coding_module_impl.cc

if WEBRTC_CODEC_AMR
DEFS += -DWEBRTC_CODEC_AMR
endif
if WEBRTC_CODEC_AMRWB
DEFS += -DWEBRTC_CODEC_AMRWB
endif
if WEBRTC_CODEC_AVT
DEFS += -DWEBRTC_CODEC_AVT
endif
if WEBRTC_CODEC_CELT
DEFS += -DWEBRTC_CODEC_CELT
endif
if WEBRTC_CODEC_G722
DEFS += -DWEBRTC_CODEC_G722
g722_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/g722/include
g722_LIB = $(top_builddir)/src/modules/audio_coding/codecs/g722/libwebrtc_codecs_g722.la
endif
if WEBRTC_CODEC_G722_1
DEFS += -DWEBRTC_CODEC_G722_1
endif
if WEBRTC_CODEC_G722_1C
DEFS += -DWEBRTC_CODEC_G722_1C
endif
if WEBRTC_CODEC_G729
DEFS += -DWEBRTC_CODEC_G729
endif
if WEBRTC_CODEC_G729_1
DEFS += -DWEBRTC_CODEC_G729_1
endif
if WEBRTC_CODEC_GSMFR
DEFS += -DWEBRTC_CODEC_GSMFR
endif
if WEBRTC_CODEC_ILBC
DEFS += -DWEBRTC_CODEC_ILBC
ilbc_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/ilbc/interface
ilbc_LIB = $(top_builddir)/src/modules/audio_coding/codecs/ilbc/libwebrtc_codecs_ilbc.la
endif
if WEBRTC_CODEC_ISAC
if WEBRTC_CODEC_ISACFX
DEFS += -DWEBRTC_CODEC_ISACFX
isac_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/iSAC/fix/interface
isac_LIB = $(top_builddir)/src/modules/audio_coding/codecs/iSAC/fix/libwebrtc_codecs_isac.la
else
DEFS += -DWEBRTC_CODEC_ISAC
isac_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/iSAC/main/interface
isac_LIB = $(top_builddir)/src/modules/audio_coding/codecs/iSAC/main/libwebrtc_codecs_isac.la
endif
endif
if WEBRTC_CODEC_OPUS
DEFS += -DWEBRTC_CODEC_OPUS
endif
if WEBRTC_CODEC_PCM16B
DEFS += -DWEBRTC_CODEC_PCM16B
pcm16b_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/pcm16b/include
pcm16b_LIB = $(top_builddir)/src/modules/audio_coding/codecs/pcm16b/libwebrtc_codecs_pcm16b.la
endif
if WEBRTC_CODEC_RED
DEFS += -DWEBRTC_CODEC_RED
endif
if WEBRTC_CODEC_SPEEX
DEFS += -DWEBRTC_CODEC_SPEEX
endif

libwebrtc_audio_coding_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/common_audio/resampler/include \
			    -I$(top_srcdir)/src/common_audio/signal_processing/include \
			    -I$(top_srcdir)/src/common_audio/vad/include \
			    -I$(top_srcdir)/src/modules/audio_coding/codecs/cng/include \
			    -I$(top_srcdir)/src/modules/audio_coding/codecs/g711/include \
			    $(g722_INCLUDE) \
			    $(ilbc_INCLUDE) \
			    $(isac_INCLUDE) \
			    $(pcm16b_INCLUDE) \
			    -I$(top_srcdir)/src/modules/audio_coding/neteq/interface \
			    -I$(top_srcdir)/src/system_wrappers/interface

libwebrtc_audio_coding_la_LIBADD = \
			    $(top_builddir)/src/common_audio/resampler/libwebrtc_resampler.la \
			    $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la \
			    $(top_builddir)/src/common_audio/vad/libwebrtc_vad.la \
			    $(top_builddir)/src/modules/audio_coding/codecs/cng/libwebrtc_codecs_cng.la \
			    $(top_builddir)/src/modules/audio_coding/codecs/g711/libwebrtc_codecs_g711.la \
			    $(g722_LIB) \
			    $(ilbc_LIB) \
			    $(isac_LIB) \
			    $(pcm16b_LIB) \
			    $(top_builddir)/src/modules/audio_coding/neteq/libwebrtc_neteq.la \
			    $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la

libwebrtc_audio_coding_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST

TESTS = audio_coding_unittest

noinst_PROGRAMS = $(TESTS)

audio_coding_unittest_SOURCES = test/ACMTest.cc \
				test/APITest.cc \
				test/Channel.cc \
				test/EncodeDecodeTest.cc \
				test/PCMFile.cc \
				test/RTPFile.cc \
				test/SpatialAudio.cc \
				test/TestAllCodecs.cc \
				test/TestFEC.cc \
				test/TestStereo.cc \
				test/TestVADDTX.cc \
				test/Tester.cc \
				test/TimedTrace.cc \
				test/TwoWayCommunication.cc \
				test/iSACTest.cc \
				test/utility.cc

audio_coding_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				 -I$(top_srcdir)/src/system_wrappers/interface \
				 -I$(top_srcdir)/test

audio_coding_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			      $(top_builddir)/src/modules/audio_coding/main/libwebrtc_audio_coding.la \
			      $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			      $(top_builddir)/test/libtest.la

endif
