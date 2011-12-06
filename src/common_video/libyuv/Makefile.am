lib_LTLIBRARIES = libwebrtc_libyuv.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./include/libyuv.h ./include/scaler.h

libwebrtc_libyuv_la_SOURCES = libyuv.cc scaler.cc
#libwebrtc_libyuv_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS)
libwebrtc_libyuv_la_CXXFLAGS = $(AM_CXXFLAGS) -I\$(top_srcdir)/src -I\$(top_srcdir)/src/modules/interface
libwebrtc_libyuv_la_LIBADD = @LIBYUV_LIBS@
libwebrtc_libyuv_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = libyuv_unittest
noinst_PROGRAMS = $(TESTS)
if WEBRTC_LINUX
linux_ldadd_ADDON = -lrt
endif
libyuv_unittest_SOURCES = libyuv_unittest.cc scaler_unittest.cc
libyuv_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			   -I$(top_srcdir)/src \
			   -I$(top_srcdir)/test \
			   -I$(top_srcdir)/src/common_video/interface
libyuv_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ $(linux_ldadd_ADDON) \
			   $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la \
			   $(top_builddir)/test/libtest.la
endif
