lib_LTLIBRARIES = libwebrtc_codecs_g711.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = include/g711_interface.h

libwebrtc_codecs_g711_la_SOURCES = g711.c g711_interface.c
libwebrtc_codecs_g711_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS)
libwebrtc_codecs_g711_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = g711_unittest
noinst_PROGRAMS = $(TESTS)

g711_unittest_SOURCES = g711_unittest.cc
g711_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				 -I$(top_srcdir)/src/system_wrappers/interface \
				 -I$(top_srcdir)/test
g711_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			      $(top_builddir)/src/modules/audio_coding/codecs/g711/libwebrtc_codecs_g711.la \
			      $(top_builddir)/test/libtest.la
endif
