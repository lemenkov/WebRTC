if WITH_TEST
TESTS =
noinst_PROGRAMS = $(TESTS) voe_cmd_test
voe_cmd_test_SOURCES = voe_cmd_test.cc

voe_cmd_test_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			-I$(top_srcdir) \
			-I$(top_srcdir)/src \
			-I$(top_srcdir)/src/voice_engine/main/interface
voe_cmd_test_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
		     $(top_builddir)/src/voice_engine/main/libwebrtc_voice_engine.la \
		     $(top_builddir)/test/libtest.la
endif
