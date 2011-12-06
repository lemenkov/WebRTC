if WITH_TEST

SUBDIRS = libtest

TESTS = test_unittest metrics_unittest
noinst_LTLIBRARIES = libtest.la libmetrics.la
noinst_PROGRAMS = $(TESTS)

libtest_la_SOURCES = run_all_unittests.cc \
		     test_suite.cc \
		     test_suite.h \
		     testsupport/fileutils.cc \
		     testsupport/frame_reader.cc \
		     testsupport/frame_writer.cc \
		     testsupport/packet_reader.cc

libtest_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) -I$(top_srcdir)

test_unittest_SOURCES = testsupport/fileutils_unittest.cc \
			testsupport/frame_reader_unittest.cc \
			testsupport/frame_writer_unittest.cc \
			testsupport/packet_reader_unittest.cc
test_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS)
test_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ $(top_builddir)/src/test/libtest.la

libmetrics_la_SOURCES = testsupport/metrics/video_metrics.cc
libmetrics_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) -I./testsupport/metrics

metrics_unittest_SOURCES = testsupport/metrics/video_metrics_unittest.cc
metrics_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS)
metrics_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			 $(top_builddir)/src/test/libtest.la \
			 $(top_builddir)/src/test/libmetrics.la \
			 $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la

endif
