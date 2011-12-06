lib_LTLIBRARIES = libwebrtc_media_file.la

DEFS += -DWEBRTC_MODULE_UTILITY_VIDEO

if WEBRTC_CODEC_AMR
DEFS += -DWEBRTC_CODEC_AMR
endif
if WEBRTC_CODEC_AMRWB
DEFS += -DWEBRTC_CODEC_AMRWB
endif
if WEBRTC_CODEC_AVT
DEFS += -DWEBRTC_CODEC_AVT
endif
if WEBRTC_CODEC_CELT
DEFS += -DWEBRTC_CODEC_CELT
endif
if WEBRTC_CODEC_G722
DEFS += -DWEBRTC_CODEC_G722
endif
if WEBRTC_CODEC_G722_1
DEFS += -DWEBRTC_CODEC_G722_1
endif
if WEBRTC_CODEC_G722_1C
DEFS += -DWEBRTC_CODEC_G722_1C
endif
if WEBRTC_CODEC_G729
DEFS += -DWEBRTC_CODEC_G729
endif
if WEBRTC_CODEC_G729_1
DEFS += -DWEBRTC_CODEC_G729_1
endif
if WEBRTC_CODEC_GSMFR
DEFS += -DWEBRTC_CODEC_GSMFR
endif
if WEBRTC_CODEC_ILBC
DEFS += -DWEBRTC_CODEC_ILBC
endif
if WEBRTC_CODEC_ISAC
if WEBRTC_CODEC_ISACFX
DEFS += -DWEBRTC_CODEC_ISACFX
else
DEFS += -DWEBRTC_CODEC_ISAC
endif
endif
if WEBRTC_CODEC_OPUS
DEFS += -DWEBRTC_CODEC_OPUS
endif
if WEBRTC_CODEC_PCM16B
DEFS += -DWEBRTC_CODEC_PCM16B
endif
if WEBRTC_CODEC_RED
DEFS += -DWEBRTC_CODEC_RED
endif
if WEBRTC_CODEC_SPEEX
DEFS += -DWEBRTC_CODEC_SPEEX
endif
if WEBRTC_CODEC_I420
DEFS += -DVIDEOCODEC_I420
endif
if WEBRTC_CODEC_VP8
DEFS += -DVIDEOCODEC_VP8
endif

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/media_file.h ./interface/media_file_defines.h

libwebrtc_media_file_la_SOURCES = \
				  source/avi_file.cc \
				  source/media_file_impl.cc \
				  source/media_file_utility.cc

libwebrtc_media_file_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/system_wrappers/interface

libwebrtc_media_file_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la

libwebrtc_media_file_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = media_file_unittest
noinst_PROGRAMS = $(TESTS)
media_file_unittest_SOURCES = source/media_file_unittest.cc
media_file_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ -I$(top_srcdir)/src -I$(top_srcdir)/test -I./source
media_file_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/media_file/libwebrtc_media_file.la \
			   $(top_builddir)/test/libtest.la
endif
