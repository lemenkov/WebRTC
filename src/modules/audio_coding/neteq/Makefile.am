lib_LTLIBRARIES = libwebrtc_neteq.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = interface/webrtc_neteq.h interface/webrtc_neteq_help_macros.h interface/webrtc_neteq_internal.h

DEFS += -DNETEQ_VOICEENGINE_CODECS -DSCRATCH

libwebrtc_neteq_la_SOURCES = \
			     accelerate.c \
			     automode.c \
			     bgn_update.c \
			     bufstats_decision.c \
			     cng_internal.c \
			     codec_db.c \
			     correlator.c \
			     dsp.c \
			     dsp_helpfunctions.c \
			     dtmf_buffer.c \
			     dtmf_tonegen.c \
			     expand.c \
			     mcu_address_init.c \
			     mcu_dsp_common.c \
			     mcu_reset.c \
			     merge.c \
			     min_distortion.c \
			     mix_voice_unvoice.c \
			     mute_signal.c \
			     normal.c \
			     packet_buffer.c \
			     peak_detection.c \
			     preemptive_expand.c \
			     random_vector.c \
			     recin.c \
			     recout.c \
			     rtcp.c \
			     rtp.c \
			     set_fs.c \
			     signal_mcu.c \
			     split_and_insert.c \
			     unmute_signal.c \
			     webrtc_neteq.c

libwebrtc_neteq_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
			    -I$(top_srcdir)/src/common_audio/signal_processing/include \
			    -I$(top_srcdir)/src/modules/audio_coding/codecs/cng/include

libwebrtc_neteq_la_LIBADD = $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la \
			  $(top_builddir)/src/modules/audio_coding/codecs/cng/libwebrtc_codecs_cng.la

libwebrtc_neteq_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
#DEFS += -DCODEC_G711 -DCODEC_CNGCODEC8 -DCODEC_CNGCODEC16 -DCODEC_CNGCODEC32 -DCODEC_CNGCODEC48
DEFS += -DCODEC_G711 -DCODEC_CNGCODEC8 -DCODEC_CNGCODEC16 -DCODEC_CNGCODEC32

if WEBRTC_CODEC_AMR
DEFS += -DCODEC_AMR
endif
if WEBRTC_CODEC_AMRWB
DEFS += -DCODEC_AMRWB
endif
if WEBRTC_CODEC_AVT
#DEFS += -DCODEC_AVT -DCODEC_ATEVENT_DECODE
DEFS += -DCODEC_ATEVENT_DECODE
endif
if WEBRTC_CODEC_CELT
DEFS += -DCODEC_CELT -DCODEC_CELT_32
endif
if WEBRTC_CODEC_G722
DEFS += -DCODEC_G722
g722_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/g722/include
g722_LIB = $(top_builddir)/src/modules/audio_coding/codecs/g722/libwebrtc_codecs_g722.la
endif
if WEBRTC_CODEC_G722_1
DEFS += -DCODEC_G722_1 -DCODEC_G722_1_16 -DCODEC_G722_1_24 -DCODEC_G722_1_32
endif
if WEBRTC_CODEC_G722_1C
DEFS += -DCODEC_G722_1C -DCODEC_G722_1C_24 -DCODEC_G722_1C_32 -DCODEC_G722_1C_48
endif
if WEBRTC_CODEC_G729
DEFS += -DCODEC_G729
endif
if WEBRTC_CODEC_G729_1
DEFS += -DCODEC_G729_1
endif
if WEBRTC_CODEC_GSMFR
#DEFS += -DCODEC_GSMFR
endif
if WEBRTC_CODEC_ILBC
DEFS += -DCODEC_ILBC
ilbc_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/ilbc/interface
ilbc_LIB = $(top_builddir)/src/modules/audio_coding/codecs/ilbc/libwebrtc_codecs_ilbc.la
endif
if WEBRTC_CODEC_ISAC
if WEBRTC_CODEC_ISACFX
DEFS += -DCODEC_ISACFX
isac_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/iSAC/fix/interface
isac_LIB = $(top_builddir)/src/modules/audio_coding/codecs/iSAC/fix/libwebrtc_codecs_isac.la
else
DEFS += -DCODEC_ISAC -DCODEC_ISAC_SWB
isac_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/iSAC/main/interface
isac_LIB = $(top_builddir)/src/modules/audio_coding/codecs/iSAC/main/libwebrtc_codecs_isac.la
endif
endif
if WEBRTC_CODEC_OPUS
DEFS += -DCODEC_OPUS
endif
if WEBRTC_CODEC_PCM16B
#DEFS += -DCODEC_PCM16B -DCODEC_PCM16B_WB -DCODEC_PCM16B_32KHZ -DCODEC_PCM16B_48KHZ
DEFS += -DCODEC_PCM16B -DCODEC_PCM16B_WB -DCODEC_PCM16B_32KHZ
pcm16b_INCLUDE = -I$(top_srcdir)/src/modules/audio_coding/codecs/pcm16b/include
pcm16b_LIB = $(top_builddir)/src/modules/audio_coding/codecs/pcm16b/libwebrtc_codecs_pcm16b.la
endif
if WEBRTC_CODEC_RED
DEFS += -DCODEC_RED
endif
if WEBRTC_CODEC_SPEEX
DEFS += -DCODEC_SPEEX -DCODEC_SPEEX_8 -DCODEC_SPEEX_16
endif

common_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			  -I$(top_srcdir)/src \
			  -I$(top_srcdir)/src/test \
			  -I./test \
			  -I$(top_srcdir)/src/system_wrappers/interface \
			  -I$(top_srcdir)/src/modules/audio_coding/codecs/cng/include \
			  -I$(top_srcdir)/src/modules/audio_coding/codecs/g711/include \
			  $(g722_INCLUDE) \
			  $(ilbc_INCLUDE) \
			  $(isac_INCLUDE) \
			  $(pcm16b_INCLUDE) \
			  -I$(top_srcdir)/src/common_audio/vad/include
common_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/audio_coding/neteq/libwebrtc_neteq.la \
			   $(top_builddir)/src/common_audio/vad/libwebrtc_vad.la \
			   $(top_builddir)/src/modules/audio_coding/codecs/cng/libwebrtc_codecs_cng.la \
			   $(top_builddir)/src/modules/audio_coding/codecs/g711/libwebrtc_codecs_g711.la \
			   $(g722_LIB) \
			   $(ilbc_LIB) \
			   $(isac_LIB) \
			   $(pcm16b_LIB) \
			   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			   $(top_builddir)/src/test/libtest.la
common_SOURCES = test/NETEQTEST_CodecClass.cc \
		 test/NETEQTEST_DummyRTPpacket.cc \
		 test/NETEQTEST_NetEQClass.cc \
		 test/NETEQTEST_RTPpacket.cc

TESTS = neteq_unittest
noinst_PROGRAMS = $(TESTS) NetEqRTPplay RTPencode RTPjitter RTPanalyze RTPchange RTPtimeshift RTPcat rtp_to_text

neteq_unittest_SOURCES = webrtc_neteq_unittest.cc $(common_SOURCES)
neteq_unittest_CXXFLAGS = $(common_CXXFLAGS)
neteq_unittest_LDADD = $(common_LDADD)

NetEqRTPplay_SOURCES = test/NetEqRTPplay.cc $(common_SOURCES)
NetEqRTPplay_CXXFLAGS = $(common_CXXFLAGS)
NetEqRTPplay_LDADD = $(common_LDADD)

RTPencode_SOURCES = test/RTPencode.cc $(common_SOURCES)
RTPencode_CXXFLAGS = $(common_CXXFLAGS)
RTPencode_LDADD = $(common_LDADD)

RTPjitter_SOURCES = test/RTPjitter.cc $(common_SOURCES)
RTPjitter_CXXFLAGS = $(common_CXXFLAGS)
RTPjitter_LDADD = $(common_LDADD)

RTPanalyze_SOURCES = test/RTPanalyze.cc $(common_SOURCES)
RTPanalyze_CXXFLAGS = $(common_CXXFLAGS)
RTPanalyze_LDADD = $(common_LDADD)

RTPchange_SOURCES = test/RTPchange.cc $(common_SOURCES)
RTPchange_CXXFLAGS = $(common_CXXFLAGS)
RTPchange_LDADD = $(common_LDADD)

RTPtimeshift_SOURCES = test/RTPtimeshift.cc $(common_SOURCES)
RTPtimeshift_CXXFLAGS = $(common_CXXFLAGS)
RTPtimeshift_LDADD = $(common_LDADD)

RTPcat_SOURCES = test/RTPcat.cc $(common_SOURCES)
RTPcat_CXXFLAGS = $(common_CXXFLAGS)
RTPcat_LDADD = $(common_LDADD)

rtp_to_text_SOURCES = test/rtp_to_text.cc $(common_SOURCES)
rtp_to_text_CXXFLAGS = $(common_CXXFLAGS)
rtp_to_text_LDADD = $(common_LDADD)

endif
