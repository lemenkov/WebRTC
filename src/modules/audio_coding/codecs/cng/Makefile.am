lib_LTLIBRARIES = libwebrtc_codecs_cng.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = include/webrtc_cng.h

libwebrtc_codecs_cng_la_SOURCES = cng_helpfuns.c webrtc_cng.c

libwebrtc_codecs_cng_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
			-I$(top_srcdir)/src/common_audio/signal_processing/include

libwebrtc_codecs_cng_la_LIBADD = $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la

libwebrtc_codecs_cng_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = cng_unittest
noinst_PROGRAMS = $(TESTS)

cng_unittest_SOURCES = cng_unittest.cc
cng_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				 -I$(top_srcdir)/src/system_wrappers/interface \
				 -I$(top_srcdir)/test
cng_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			      $(top_builddir)/src/modules/audio_coding/codecs/cng/libwebrtc_codecs_cng.la \
			      $(top_builddir)/test/libtest.la
endif
