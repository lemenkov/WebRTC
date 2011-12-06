lib_LTLIBRARIES = libwebrtc_remote_bitrate_estimator.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./include/remote_bitrate_estimator.h

libwebrtc_remote_bitrate_estimator_la_SOURCES = bitrate_estimator.cc \
						overuse_detector.cc \
						remote_bitrate_estimator.cc \
						remote_rate_control.cc

libwebrtc_remote_bitrate_estimator_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/modules/rtp_rtcp/interface \
			    -I$(top_srcdir)/src/system_wrappers/interface

libwebrtc_remote_bitrate_estimator_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la

libwebrtc_remote_bitrate_estimator_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = remote_bitrate_estimator_unittest
noinst_PROGRAMS = $(TESTS)
remote_bitrate_estimator_unittest_SOURCES = bitrate_estimator_unittest.cc remote_bitrate_estimator_unittest.cc
remote_bitrate_estimator_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ -I$(top_srcdir)/src -I$(top_srcdir)/test -I./source
remote_bitrate_estimator_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/remote_bitrate_estimator/libwebrtc_remote_bitrate_estimator.la \
			   $(top_builddir)/test/libtest.la
endif
