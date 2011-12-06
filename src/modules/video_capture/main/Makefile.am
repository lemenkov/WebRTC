lib_LTLIBRARIES = libwebrtc_video_capture.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/video_capture.h ./interface/video_capture_defines.h ./interface/video_capture_factory.h

if WEBRTC_LINUX
linux_INCLUDES = -I./source/Linux
linux_SOURCES = \
		source/Linux/device_info_linux.cc \
		source/Linux/video_capture_linux.cc
endif

if WEBRTC_MAC
mac_INCLUDES = -I./source/Mac -I./source/Mac/QuickTime -I./source/Mac -I./source/Mac/QTKit
mac_SOURCES = \
	      source/Mac/QTKit/video_capture_qtkit.mm \
	      source/Mac/QTKit/video_capture_qtkit_info.mm \
	      source/Mac/QTKit/video_capture_qtkit_info_objc.mm \
	      source/Mac/QTKit/video_capture_qtkit_objc.mm \
	      source/Mac/QTKit/video_capture_recursive_lock.mm \
	      source/Mac/video_capture_mac.mm
endif

if WEBRTC_WINDOWS
windows_INCLUDES = -I./source/Windows
windows_SOURCES = \
		  source/Windows/device_info_windows.cc \
		  source/Windows/help_functions_windows.cc \
		  source/Windows/sink_filter_windows.cc \
		  source/Windows/video_capture_factory_windows.cc \
		  source/Windows/video_capture_windows.cc
endif

#external_SOURCES = \
#		   source/External/device_info_external.cc \
#		   source/External/video_capture_external.cc

libwebrtc_video_capture_la_SOURCES = \
				     source/device_info_impl.cc \
				     source/video_capture_factory.cc \
				     source/video_capture_impl.cc \
				     $(mac_SOURCES) \
				     $(linux_SOURCES) \
				     $(windows_SOURCES)

libwebrtc_video_capture_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
				      -I$(top_srcdir)/src/system_wrappers/interface \
				      $(linux_INCLUDES) \
				      $(mac_INCLUDES) \
				      $(windows_INCLUDES)

libwebrtc_video_capture_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
				       $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la

libwebrtc_video_capture_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if FALSE
#if WITH_TEST
TESTS = video_capture_unittest
noinst_PROGRAMS = $(TESTS)
video_capture_unittest_SOURCES = test/video_capture_unittest.cc
video_capture_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				  -I$(top_srcdir)/src -I$(top_srcdir)/src/test -I./source \
				  -I$(top_srcdir)/src/modules/utility/interface \
				  -I$(top_srcdir)/src/system_wrappers/interface

video_capture_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/video_capture/main/libwebrtc_video_capture.la \
			   $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
			   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			   $(top_builddir)/src/test/libtest.la
endif
