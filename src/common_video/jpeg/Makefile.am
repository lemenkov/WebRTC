lib_LTLIBRARIES = libwebrtc_jpeg.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = include/jpeg.h

DEFS += -DUSE_SYSTEM_LIBJPEG

libwebrtc_jpeg_la_SOURCES = data_manager.cc jpeg.cc
libwebrtc_jpeg_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			     -I$(top_srcdir)/src/common_video/interface
libwebrtc_jpeg_la_LIBADD = @LIBJPEG_LIBS@
libwebrtc_jpeg_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)


if WITH_TEST
TESTS = jpeg_unittest
noinst_PROGRAMS = $(TESTS)
jpeg_unittest_SOURCES = jpeg_unittest.cc
jpeg_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			 -I$(top_srcdir)/src \
			 -I$(top_srcdir)/src/test \
			 -I$(top_srcdir)/src/common_video/interface
jpeg_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
		      $(top_builddir)/src/common_video/jpeg/libwebrtc_jpeg.la \
		      $(top_builddir)/src/test/libtest.la
endif
