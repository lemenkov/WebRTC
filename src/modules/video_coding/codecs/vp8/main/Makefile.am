lib_LTLIBRARIES = libwebrtc_codecs_vp8.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = interface/vp8.h interface/vp8_common_types.h

libwebrtc_codecs_vp8_la_SOURCES = \
				  source/reference_picture_selection.cc \
				  source/temporal_layers.cc \
				  source/vp8.cc

libwebrtc_codecs_vp8_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @LIBVPX_CXXFLAGS@ -DWEBRTC_LIBVPX_VERSION=@LIBVPX_VERSION@ \
				  -I$(top_srcdir)/src/common_video/interface \
				  -I$(top_srcdir)/src/common_video/libyuv/include \
				  -I$(top_srcdir)/src/modules/interface \
				  -I$(top_srcdir)/src/modules/video_coding/codecs/interface \
				  -I$(top_srcdir)/src/system_wrappers/interface
libwebrtc_codecs_vp8_la_LIBADD = @LIBVPX_LIBS@ \
			    $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la \
			    $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la
libwebrtc_codecs_vp8_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST

TESTS = vp8_unittest
noinst_PROGRAMS = $(TESTS) vp8_test
vp8_unittest_SOURCES =  source/temporal_layers_unittest.cc \
			source/reference_picture_selection_unittest.cc
vp8_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			-I$(top_srcdir)/src/modules/video_coding/codecs/interface
vp8_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
		     $(top_builddir)/src/modules/video_coding/codecs/vp8/main/libwebrtc_codecs_vp8.la \
		     $(top_builddir)/test/libtest.la

vp8_test_SOURCES = test/benchmark.cc \
		   test/dual_decoder_test.cc \
		   test/normal_async_test.cc \
		   test/packet_loss_test.cc \
		   test/rps_test.cc \
		   test/tester.cc \
		   test/unit_test.cc
vp8_test_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
		    -I$(top_srcdir)/src/modules/video_coding/codecs/interface \
		    -I$(top_srcdir)/src/system_wrappers/interface \
		    -I$(top_srcdir)/test \
		    -I$(top_srcdir)/src/common_video/interface
vp8_test_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
		 $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
		 $(top_builddir)/src/modules/video_coding/main/libwebrtc_video_coding.la \
		 $(top_builddir)/src/modules/video_coding/codecs/test_framework/libtest_framework.la \
		 $(top_builddir)/test/libmetrics.la \
		 $(top_builddir)/test/libtest.la
endif
