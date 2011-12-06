lib_LTLIBRARIES = libwebrtc_video_engine.la

if WEBRTC_CODEC_I420
DEFS += -DVIDEOCODEC_I420
endif
if WEBRTC_CODEC_VP8
DEFS += -DVIDEOCODEC_VP8
endif

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = \
			include/vie_base.h \
			include/vie_capture.h \
			include/vie_codec.h \
			include/vie_encryption.h \
			include/vie_errors.h \
			include/vie_external_codec.h \
			include/vie_file.h \
			include/vie_image_process.h \
			include/vie_network.h \
			include/vie_render.h \
			include/vie_rtp_rtcp.h

libwebrtc_video_engine_la_SOURCES = \
				    stream_synchronization.cc \
				    vie_base_impl.cc \
				    vie_capture_impl.cc \
				    vie_capturer.cc \
				    vie_channel.cc \
				    vie_channel_group.cc \
				    vie_channel_manager.cc \
				    vie_codec_impl.cc \
				    vie_encoder.cc \
				    vie_encryption_impl.cc \
				    vie_external_codec_impl.cc \
				    vie_file_image.cc \
				    vie_file_impl.cc \
				    vie_file_player.cc \
				    vie_file_recorder.cc \
				    vie_frame_provider_base.cc \
				    vie_image_process_impl.cc \
				    vie_impl.cc \
				    vie_input_manager.cc \
				    vie_manager_base.cc \
				    vie_network_impl.cc \
				    vie_performance_monitor.cc \
				    vie_receiver.cc \
				    vie_ref_count.cc \
				    vie_remb.cc \
				    vie_render_impl.cc \
				    vie_render_manager.cc \
				    vie_renderer.cc \
				    vie_rtp_rtcp_impl.cc \
				    vie_sender.cc \
				    vie_shared_data.cc \
				    vie_sync_module.cc

libwebrtc_video_engine_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/common_video/interface \
			    -I$(top_srcdir)/src/modules/media_file/interface \
			    -I$(top_srcdir)/src/modules/audio_coding/main/interface \
			    -I$(top_srcdir)/src/modules/video_coding/main/interface \
			    -I$(top_srcdir)/src/modules/video_coding/codecs/interface \
			    -I$(top_srcdir)/src/modules/video_processing/main/interface \
			    -I$(top_srcdir)/src/modules/video_render/main/interface \
			    -I$(top_srcdir)/src/modules/rtp_rtcp/interface \
			    -I$(top_srcdir)/src/modules/udp_transport/interface \
			    -I$(top_srcdir)/src/modules/utility/interface \
			    -I$(top_srcdir)/src/voice_engine/main/interface \
			    -I$(top_srcdir)/src/system_wrappers/interface

libwebrtc_video_engine_la_LIBADD = \
				   $(top_builddir)/src/common_video/libyuv/libwebrtc_libyuv.la \
				   $(top_builddir)/src/common_video/jpeg/libwebrtc_jpeg.la \
				   $(top_builddir)/src/modules/media_file/libwebrtc_media_file.la \
				   $(top_builddir)/src/modules/rtp_rtcp/libwebrtc_rtp_rtcp.la \
				   $(top_builddir)/src/modules/bitrate_controller/libwebrtc_bitrate_controller.la \
				   $(top_builddir)/src/modules/udp_transport/libwebrtc_udp_transport.la \
				   $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
				   $(top_builddir)/src/modules/video_capture/main/libwebrtc_video_capture.la \
				   $(top_builddir)/src/modules/video_coding/main/libwebrtc_video_coding.la \
				   $(top_builddir)/src/modules/video_processing/main/libwebrtc_video_processing.la \
				   $(top_builddir)/src/modules/video_render/main/libwebrtc_video_render.la \
				   $(top_builddir)/src/voice_engine/main/libwebrtc_voice_engine.la \
				   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la

libwebrtc_video_engine_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = video_engine_unittest
noinst_PROGRAMS = $(TESTS)
video_engine_unittest_SOURCES = vie_remb_unittest.cc stream_synchronization_unittest.cc
video_engine_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				 -I$(top_srcdir)/src/test \
				 -I$(top_srcdir)/src
video_engine_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			   $(top_builddir)/src/video_engine/libwebrtc_video_engine.la \
			   $(top_builddir)/src/modules/rtp_rtcp/libwebrtc_rtp_rtcp.la \
			   $(top_builddir)/src/test/libtest.la
SUBDIRS = test
endif
