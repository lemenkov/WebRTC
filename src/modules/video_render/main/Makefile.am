lib_LTLIBRARIES = libwebrtc_video_render.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/video_render.h ./interface/video_render_defines.h

if WEBRTC_LINUX
linux_INCLUDES = -I./source/linux
linux_SOURCES = \
		source/linux/video_render_linux_impl.cc \
		source/linux/video_x11_channel.cc \
		source/linux/video_x11_render.cc
linux_CXXFLAGS = $(LIBX11_CXXFLAGS) $(LIBXEXT_CXXFLAGS)
linux_LIBADD = $(LIBX11_LIBS) $(LIBXEXT_LIBS)
endif

if WEBRTC_MAC
mac_INCLUDES = -I./source/mac
mac_SOURCES = \
	      source/mac/cocoa_full_screen_window.mm \
	      source/mac/cocoa_render_view.mm \
	      source/mac/video_render_agl.cc \
	      source/mac/video_render_mac_carbon_impl.cc \
	      source/mac/video_render_mac_cocoa_impl.mm \
	      source/mac/video_render_nsopengl.mm
mac_CXXFLAGS =
mac_LIBADD =
endif

if WEBRTC_WINDOWS
windows_INCLUDES = -I./source/windows
windows_SOURCES = \
		  source/windows/video_render_direct3d9.cc \
		  source/windows/video_render_directdraw.cc \
		  source/windows/video_render_windows_impl.cc
windows_CXXFLAGS =
windows_LIBADD =
endif

# FIXME
#DEFS += -DWEBRTC_INCLUDE_INTERNAL_VIDEO_RENDER
external_SOURCES = source/external/video_render_external_impl.cc

libwebrtc_video_render_la_SOURCES = source/incoming_video_stream.cc \
				    source/video_render_frames.cc \
				    source/video_render_impl.cc \
				    $(external_SOURCES) \
				    $(linux_SOURCES) \
				    $(mac_SOURCES) \
				    $(windows_SOURCES)

libwebrtc_video_render_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
				     -I$(top_srcdir)/src/system_wrappers/interface $(addon_INCLUDES) -I./source \
				     $(linux_INCLUDES) $(linux_CXXFLAGS) \
				     $(mac_INCLUDES) $(mac_CXXFLAGS) \
				     $(windows_INCLUDES) $(windows_CXXFLAGS)

libwebrtc_video_render_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
				   $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la \
				   $(linux_LIBADD) \
				   $(mac_LIBADD) \
				   $(windows_LIBADD)

libwebrtc_video_render_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS =
noinst_PROGRAMS = video_render_module_test
video_render_module_test_SOURCES = test/testAPI/testAPI.cc
video_render_module_test_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ @LIBX11_CXXFLAGS@ @LIBXEXT_CXXFLAGS@ \
				 -I$(top_srcdir)/src -I$(top_srcdir)/src/test -I./source -I./test/testAPI \
				 -I$(top_srcdir)/src/modules/utility/interface \
				 -I$(top_srcdir)/src/common_video/libyuv/include \
				 -I$(top_srcdir)/src/system_wrappers/interface
video_render_module_test_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ @LIBX11_LIBS@ @LIBXEXT_LIBS@ -lpthread -lm -lrt \
			   $(top_builddir)/src/modules/video_render/main/libwebrtc_video_render.la \
			   $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la \
			   $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
			   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			   $(top_builddir)/src/test/libtest.la
endif
