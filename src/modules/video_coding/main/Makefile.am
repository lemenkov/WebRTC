lib_LTLIBRARIES = libwebrtc_video_coding.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/video_coding.h ./interface/video_coding_defines.h

if WEBRTC_CODEC_I420
DEFS += -DVIDEOCODEC_I420
i420_LIBS = $(top_builddir)/src/modules/video_coding/codecs/i420/main/libwebrtc_codecs_i420.la
i420_INCLUDES = -I$(top_srcdir)/src/modules/video_coding/codecs/i420/main/interface
endif
if WEBRTC_CODEC_VP8
DEFS += -DVIDEOCODEC_VP8
vp8_LIBS = $(top_builddir)/src/modules/video_coding/codecs/vp8/main/libwebrtc_codecs_vp8.la
vp8_INCLUDES =  -I$(top_srcdir)/src/modules/video_coding/codecs/vp8/main/interface
endif

libwebrtc_video_coding_la_SOURCES = \
				    source/codec_database.cc \
				    source/codec_timer.cc \
				    source/content_metrics_processing.cc \
				    source/decoding_state.cc \
				    source/encoded_frame.cc \
				    source/exp_filter.cc \
				    source/frame_buffer.cc \
				    source/frame_dropper.cc \
				    source/generic_decoder.cc \
				    source/generic_encoder.cc \
				    source/inter_frame_delay.cc \
				    source/jitter_buffer.cc \
				    source/jitter_buffer_common.cc \
				    source/jitter_estimator.cc \
				    source/media_opt_util.cc \
				    source/media_optimization.cc \
				    source/packet.cc \
				    source/qm_select.cc \
				    source/receiver.cc \
				    source/rtt_filter.cc \
				    source/session_info.cc \
				    source/timestamp_extrapolator.cc \
				    source/timestamp_map.cc \
				    source/timing.cc \
				    source/video_coding_impl.cc


libwebrtc_video_coding_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/common_video/interface \
			    -I$(top_srcdir)/src/common_video/libyuv/include \
			    -I$(top_srcdir)/src/modules/video_coding/codecs/interface \
			    $(i420_INCLUDES) \
			    $(vp8_INCLUDES) \
			    -I$(top_srcdir)/src/modules/video_coding/codecs/i420/main/interface \
			    -I$(top_srcdir)/src/modules/video_coding/codecs/vp8/main/interface \
			    -I$(top_srcdir)/src/system_wrappers/interface

libwebrtc_video_coding_la_LIBADD = \
			    $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la \
			    $(i420_LIBS) \
			    $(vp8_LIBS) \
			    $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la

libwebrtc_video_coding_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = video_coding_unittest
noinst_PROGRAMS = $(TESTS) video_coding_test
video_coding_unittest_SOURCES = source/decoding_state_unittest.cc \
				source/jitter_buffer_unittest.cc \
				source/qm_select_unittest.cc \
				source/session_info_unittest.cc \
				source/video_coding_robustness_unittest.cc

video_coding_test_SOURCES = test/codec_database_test.cc \
			    test/decode_from_storage_test.cc \
			    test/generic_codec_test.cc \
			    test/jitter_buffer_test.cc \
			    test/media_opt_test.cc \
			    test/mt_test_common.cc \
			    test/mt_rx_tx_test.cc \
			    test/normal_test.cc \
			    test/quality_modes_test.cc \
			    test/receiver_timing_tests.cc \
			    test/rtp_player.cc \
			    test/test_callbacks.cc \
			    test/test_util.cc \
			    test/tester_main.cc \
			    test/video_rtp_play_mt.cc \
			    test/video_rtp_play.cc \
			    test/video_source.cc

video_coding_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			    -I$(top_srcdir)/src/system_wrappers/interface \
			    -I$(top_srcdir)/src -I$(top_srcdir)/src/test -I./source
video_coding_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/video_coding/main/libwebrtc_video_coding.la \
			   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			   $(top_builddir)/src/test/libtest.la

video_coding_test_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			    -I$(top_srcdir)/src/system_wrappers/interface \
			    $(vp8_INCLUDES) \
			    -I$(top_srcdir)/src/modules/video_coding/codecs/interface \
			    -I$(top_srcdir)/src/modules/utility/interface \
			    -I$(top_srcdir)/src/modules/video_processing/main/interface \
			    -I$(top_srcdir)/src/modules/rtp_rtcp/interface \
			    -I$(top_srcdir)/src -I$(top_srcdir)/src/test -I./source
video_coding_test_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la \
			   $(top_builddir)/src/modules/rtp_rtcp/libwebrtc_rtp_rtcp.la \
			   $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
			   $(vp8_LIBS) \
			   $(top_builddir)/src/modules/video_coding/main/libwebrtc_video_coding.la \
			   $(top_builddir)/src/modules/video_processing/main/libwebrtc_video_processing.la \
			   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			   $(top_builddir)/src/test/libmetrics.la \
			   $(top_builddir)/src/test/libtest.la
endif
