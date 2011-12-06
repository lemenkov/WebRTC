lib_LTLIBRARIES = libwebrtc_audio_conference_mixer.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/audio_conference_mixer.h ./interface/audio_conference_mixer_defines.h

libwebrtc_audio_conference_mixer_la_SOURCES = \
				   source/audio_conference_mixer_impl.cc \
				   source/audio_frame_manipulator.cc \
				   source/level_indicator.cc \
				   source/time_scheduler.cc

libwebrtc_audio_conference_mixer_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/system_wrappers/interface \
			    -I$(top_srcdir)/src/modules/audio_processing/include

libwebrtc_audio_conference_mixer_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
					     $(top_builddir)/src/modules/audio_processing/libwebrtc_audio_processing.la

libwebrtc_audio_conference_mixer_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = audio_conference_mixer_unittest
noinst_PROGRAMS = $(TESTS)
audio_conference_mixer_unittest_SOURCES = source/audio_conference_mixer_unittest.cc
audio_conference_mixer_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
					   -I$(top_srcdir)/src -I$(top_srcdir)/src/test -I./source -I./interface \
					   -I$(top_srcdir)/src/system_wrappers/interface
audio_conference_mixer_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/audio_conference_mixer/libwebrtc_audio_conference_mixer.la \
			   $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
			   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			   $(top_builddir)/src/test/libtest.la
endif
