lib_LTLIBRARIES = libwebrtc_vad.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./include/webrtc_vad.h

libwebrtc_vad_la_SOURCES = vad_core.c \
		    vad_filterbank.c \
		    vad_gmm.c \
		    vad_sp.c \
		    webrtc_vad.c

libwebrtc_vad_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
		   -I$(top_srcdir)/src/common_audio/signal_processing/include
libwebrtc_vad_la_LIBADD = $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la
libwebrtc_vad_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = vad_unittest
noinst_PROGRAMS = $(TESTS)
vad_unittest_SOURCES = vad_core_unittest.cc \
		       vad_filterbank_unittest.cc \
		       vad_gmm_unittest.cc \
		       vad_sp_unittest.cc \
		       vad_unittest.cc
vad_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ -I$(top_srcdir)/src/common_audio/signal_processing/include -I$(top_srcdir)/src/common_audio/vad/include -I$(top_srcdir)
vad_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/common_audio/vad/libwebrtc_vad.la \
			   $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la \
			   $(top_builddir)/src/test/libtest.la
endif
