lib_LTLIBRARIES = libwebrtc_video_processing.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/video_processing.h ./interface/video_processing_defines.h

if WITH_SSE2
sse2_SOURCES = source/content_analysis_sse2.cc
endif

libwebrtc_video_processing_la_SOURCES = \
					source/brighten.cc \
					source/brightness_detection.cc \
					source/color_enhancement.cc \
					source/content_analysis.cc \
					source/deflickering.cc \
					source/denoising.cc \
					source/frame_preprocessor.cc \
					source/spatial_resampler.cc \
					source/video_decimator.cc \
					source/video_processing_impl.cc \
					$(sse2_SOURCES)

libwebrtc_video_processing_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/system_wrappers/interface \
			    -I$(top_srcdir)/src/common_audio/signal_processing/include

libwebrtc_video_processing_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
				       $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la \
				       $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la

libwebrtc_video_processing_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = video_processing_unittest
noinst_PROGRAMS = $(TESTS)
video_processing_unittest_SOURCES = test/unit_test/brightness_detection_test.cc \
				    test/unit_test/color_enhancement_test.cc \
				    test/unit_test/content_metrics_test.cc \
				    test/unit_test/deflickering_test.cc \
				    test/unit_test/denoising_test.cc \
				    test/unit_test/unit_test.cc
video_processing_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				  -I$(top_srcdir)/src -I$(top_srcdir)/test -I./test/unit_test \
				  -I$(top_srcdir)/src/modules/utility/interface \
				  -I$(top_srcdir)/src/modules/video_processing/main/interface

video_processing_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/video_processing/main/libwebrtc_video_processing.la \
			   $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
			   $(top_builddir)/test/libtest.la
endif
