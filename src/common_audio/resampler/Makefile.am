lib_LTLIBRARIES = libwebrtc_resampler.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./include/resampler.h

libwebrtc_resampler_la_SOURCES = resampler.cc
libwebrtc_resampler_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
		   -I$(top_srcdir)/src/common_audio/signal_processing/include
libwebrtc_resampler_la_LIBADD = $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la
libwebrtc_resampler_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = resampler_unittest
noinst_PROGRAMS = $(TESTS)
resampler_unittest_SOURCES = resampler_unittest.cc
resampler_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ -I$(top_srcdir)/src/common_audio/resampler/include -I$(top_srcdir)
resampler_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/common_audio/resampler/libwebrtc_resampler.la \
			   $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la \
			   $(top_builddir)/src/test/libtest.la
endif
