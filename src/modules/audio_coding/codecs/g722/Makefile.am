if WEBRTC_CODEC_G722

lib_LTLIBRARIES = libwebrtc_codecs_g722.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = include/g722_interface.h

libwebrtc_codecs_g722_la_SOURCES = g722_decode.c g722_encode.c g722_interface.c

libwebrtc_codecs_g722_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS)
libwebrtc_codecs_g722_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = g722_unittest
noinst_PROGRAMS = $(TESTS)

g722_unittest_SOURCES = g722_unittest.cc
g722_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				 -I$(top_srcdir)/src/system_wrappers/interface \
				 -I$(top_srcdir)/src/test
g722_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			      $(top_builddir)/src/modules/audio_coding/codecs/g722/libwebrtc_codecs_g722.la \
			      $(top_builddir)/src/test/libtest.la
endif
endif
