if WITH_TEST

TESTS = video_codecs_test_framework_unittest
noinst_LTLIBRARIES = libvideo_codecs_test_framework.la
noinst_PROGRAMS = $(TESTS)

libvideo_codecs_test_framework_la_SOURCES = packet_manipulator.cc \
					   predictive_packet_manipulator.cc \
					   stats.cc \
					   videoprocessor.cc

libvideo_codecs_test_framework_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
					     -I$(top_srcdir)/test

video_codecs_test_framework_unittest_SOURCES = packet_manipulator_unittest.cc \
					       stats_unittest.cc \
					       videoprocessor_unittest.cc

video_codecs_test_framework_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
						-I$(top_srcdir)/test
video_codecs_test_framework_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
					     $(top_builddir)/src/modules/video_coding/codecs/test/libvideo_codecs_test_framework.la \
					     $(top_builddir)/src/modules/video_coding/main/libwebrtc_video_coding.la \
					     $(top_builddir)/test/libtest.la

endif
