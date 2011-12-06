if WITH_TEST

noinst_LTLIBRARIES = libtest_framework.la

libtest_framework_la_SOURCES = benchmark.cc \
			       normal_async_test.cc \
			       normal_test.cc \
			       packet_loss_test.cc \
			       performance_test.cc \
			       test.cc \
			       unit_test.cc \
			       video_buffer.cc \
			       video_source.cc

libtest_framework_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
				-I$(top_srcdir)/src/common_video/interface \
				-I$(top_srcdir)/src/modules/video_coding/codecs/interface \
				-I$(top_srcdir)/src/system_wrappers/interface \
				-I$(top_srcdir)/src/test

endif
