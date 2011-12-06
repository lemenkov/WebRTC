lib_LTLIBRARIES = libwebrtc_codecs_i420.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = interface/i420.h

libwebrtc_codecs_i420_la_SOURCES = source/i420.cc
libwebrtc_codecs_i420_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
				  -I$(top_srcdir)/src/common_video/interface \
				  -I$(top_srcdir)/src/modules/video_coding/codecs/interface \
				  -I$(top_srcdir)/src/system_wrappers/interface
libwebrtc_codecs_i420_la_LIBADD = \
			    $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la
libwebrtc_codecs_i420_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)
