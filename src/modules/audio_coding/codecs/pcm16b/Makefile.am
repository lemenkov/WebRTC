if WEBRTC_CODEC_PCM16B

lib_LTLIBRARIES = libwebrtc_codecs_pcm16b.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = include/pcm16b.h

libwebrtc_codecs_pcm16b_la_SOURCES = pcm16b.c
libwebrtc_codecs_pcm16b_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
				    -I$(top_srcdir)/src/common_audio/signal_processing/include
libwebrtc_codecs_pcm16b_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = pcm16b_unittest
noinst_PROGRAMS = $(TESTS)

pcm16b_unittest_SOURCES = pcm16b_unittest.cc
pcm16b_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				 -I$(top_srcdir)/src/system_wrappers/interface \
				 -I$(top_srcdir)/test
pcm16b_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			      $(top_builddir)/src/modules/audio_coding/codecs/pcm16b/libwebrtc_codecs_pcm16b.la \
			      $(top_builddir)/test/libtest.la
endif
endif
