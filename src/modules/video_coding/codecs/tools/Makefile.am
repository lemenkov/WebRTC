if WITH_TEST

if WEBRTC_CODEC_I420
DEFS += -DVIDEOCODEC_I420
endif

if WEBRTC_CODEC_VP8
DEFS += -DVIDEOCODEC_VP8
endif

noinst_PROGRAMS = video_quality_measurement

video_quality_measurement_SOURCES = video_quality_measurement.cc
video_quality_measurement_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
				     -I$(top_srcdir)/src/test \
				     -I$(top_srcdir)/src/modules/video_coding/codecs/interface
video_quality_measurement_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ @GFLAGS_LIBS@ \
				  $(top_builddir)/src/test/libtest.la \
				  $(top_builddir)/src/test/libmetrics.la \
				  $(top_builddir)/src/modules/video_coding/codecs/test_framework/libtest_framework.la \
				  $(top_builddir)/src/modules/video_coding/codecs/test/libvideo_codecs_test_framework.la \
				  $(top_builddir)/src/modules/video_coding/main/libwebrtc_video_coding.la

endif
