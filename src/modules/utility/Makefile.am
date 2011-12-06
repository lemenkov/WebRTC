lib_LTLIBRARIES = libwebrtc_utility.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/file_player.h ./interface/file_recorder.h ./interface/process_thread.h ./interface/rtp_dump.h

# FIXME
#if WEBRTC_MODULE_UTILITY_VIDEO
video_SOURCES = \
		source/frame_scaler.cc \
		source/video_coder.cc \
		source/video_frames_queue.cc
DEFS += -DWEBRTC_MODULE_UTILITY_VIDEO
#endif

libwebrtc_utility_la_SOURCES = \
			       source/audio_frame_operations.cc \
			       source/coder.cc \
			       source/file_player_impl.cc \
			       source/file_recorder_impl.cc \
			       source/process_thread_impl.cc \
			       source/rtp_dump_impl.cc \
			       $(video_SOURCES)

libwebrtc_utility_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/common_audio/resampler/include \
			    -I$(top_srcdir)/src/modules/audio_coding/main/interface \
			    -I$(top_srcdir)/src/modules/media_file/interface \
			    -I$(top_srcdir)/src/modules/video_coding/main/interface \
			    -I$(top_srcdir)/src/system_wrappers/interface

libwebrtc_utility_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			      $(top_builddir)/src/common_audio/resampler/libwebrtc_resampler.la \
			      $(top_builddir)/src/modules/audio_coding/main/libwebrtc_audio_coding.la \
			      $(top_builddir)/src/modules/video_coding/main/libwebrtc_video_coding.la \
			      $(top_builddir)/src/modules/media_file/libwebrtc_media_file.la

libwebrtc_utility_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = utility_unittest
noinst_PROGRAMS = $(TESTS)
utility_unittest_SOURCES = source/file_player_unittest.cc
utility_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ -I$(top_srcdir)/src -I$(top_srcdir)/src/test -I./source
utility_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			 $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
			 $(top_builddir)/src/test/libtest.la

if FALSE
# TODO
# source/audio_frame_operations_unittest.cc
utility_test_api_SOURCES = test/testAPI.cc
utility_test_api_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			    -I$(top_srcdir)/src -I$(top_srcdir)/src/test -I./source \
			    -I$(top_srcdir)/src/modules/media_file/interface \
			    -I$(top_srcdir)/src/modules/audio_coding/main/interface \
			    -I$(top_srcdir)/src/system_wrappers/interface
utility_test_api_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			 $(top_builddir)/src/modules/audio_coding/main/libwebrtc_audio_coding.la \
			 $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
			 $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			 $(top_builddir)/src/modules/media_file/libwebrtc_media_file.la \
			 $(top_builddir)/src/test/libtest.la
endif
endif
