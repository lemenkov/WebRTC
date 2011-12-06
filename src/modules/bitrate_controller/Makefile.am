lib_LTLIBRARIES = libwebrtc_bitrate_controller.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./include/bitrate_controller.h

libwebrtc_bitrate_controller_la_SOURCES = bitrate_controller_impl.cc \
					  send_side_bandwidth_estimation.cc

libwebrtc_bitrate_controller_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/system_wrappers/interface

libwebrtc_bitrate_controller_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la

libwebrtc_bitrate_controller_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = bitrate_controller_unittest
noinst_PROGRAMS = $(TESTS)
bitrate_controller_unittest_SOURCES = bitrate_controller_unittest.cc
bitrate_controller_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ -I$(top_srcdir)/src -I$(top_srcdir)/test -I./source
bitrate_controller_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/bitrate_controller/libwebrtc_bitrate_controller.la \
			   $(top_builddir)/test/libtest.la
endif
