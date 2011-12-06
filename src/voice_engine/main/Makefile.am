lib_LTLIBRARIES = libwebrtc_voice_engine.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = \
			./interface/voe_audio_processing.h \
			./interface/voe_base.h \
			./interface/voe_call_report.h \
			./interface/voe_codec.h \
			./interface/voe_dtmf.h \
			./interface/voe_encryption.h \
			./interface/voe_errors.h \
			./interface/voe_external_media.h \
			./interface/voe_file.h \
			./interface/voe_hardware.h \
			./interface/voe_neteq_stats.h \
			./interface/voe_network.h \
			./interface/voe_rtp_rtcp.h \
			./interface/voe_video_sync.h \
			./interface/voe_volume_control.h

libwebrtc_voice_engine_la_SOURCES = \
				    source/channel.cc \
				    source/channel_manager.cc \
				    source/channel_manager_base.cc \
				    source/dtmf_inband.cc \
				    source/dtmf_inband_queue.cc \
				    source/level_indicator.cc \
				    source/monitor_module.cc \
				    source/output_mixer.cc \
				    source/output_mixer_internal.cc \
				    source/shared_data.cc \
				    source/statistics.cc \
				    source/transmit_mixer.cc \
				    source/utility.cc \
				    source/voe_audio_processing_impl.cc \
				    source/voe_base_impl.cc \
				    source/voe_call_report_impl.cc \
				    source/voe_codec_impl.cc \
				    source/voe_dtmf_impl.cc \
				    source/voe_encryption_impl.cc \
				    source/voe_external_media_impl.cc \
				    source/voe_file_impl.cc \
				    source/voe_hardware_impl.cc \
				    source/voe_neteq_stats_impl.cc \
				    source/voe_network_impl.cc \
				    source/voe_rtp_rtcp_impl.cc \
				    source/voe_video_sync_impl.cc \
				    source/voe_volume_control_impl.cc \
				    source/voice_engine_impl.cc
libwebrtc_voice_engine_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/common_audio/resampler/include \
			    -I$(top_srcdir)/src/common_audio/signal_processing/include \
			    -I$(top_srcdir)/src/modules/audio_coding/main/interface \
			    -I$(top_srcdir)/src/modules/audio_conference_mixer/interface \
			    -I$(top_srcdir)/src/modules/audio_device/main/interface \
			    -I$(top_srcdir)/src/modules/audio_device/main/source \
			    -I$(top_srcdir)/src/modules/audio_processing/include \
			    -I$(top_srcdir)/src/modules/media_file/interface \
			    -I$(top_srcdir)/src/modules/rtp_rtcp/interface \
			    -I$(top_srcdir)/src/modules/udp_transport/interface \
			    -I$(top_srcdir)/src/modules/utility/interface \
			    -I$(top_srcdir)/src/system_wrappers/interface

libwebrtc_voice_engine_la_LIBADD = \
				   $(top_builddir)/src/common_audio/resampler/libwebrtc_resampler.la \
				   $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la \
				   $(top_builddir)/src/modules/audio_coding/main/libwebrtc_audio_coding.la \
				   $(top_builddir)/src/modules/audio_conference_mixer/libwebrtc_audio_conference_mixer.la \
				   $(top_builddir)/src/modules/audio_device/main/libwebrtc_audio_device.la \
				   $(top_builddir)/src/modules/audio_processing/libwebrtc_audio_processing.la \
				   $(top_builddir)/src/modules/media_file/libwebrtc_media_file.la \
				   $(top_builddir)/src/modules/rtp_rtcp/libwebrtc_rtp_rtcp.la \
				   $(top_builddir)/src/modules/udp_transport/libwebrtc_udp_transport.la \
				   $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
				   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la

libwebrtc_voice_engine_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = voice_engine_unittest
noinst_PROGRAMS = $(TESTS)
voice_engine_unittest_SOURCES = source/channel_unittest.cc source/output_mixer_unittest.cc

voice_engine_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				 -I$(top_srcdir)/src/common_audio/resampler/include \
				 -I$(top_srcdir)/src/common_audio/signal_processing/include \
				 -I$(top_srcdir)/src/modules/audio_coding/main/interface \
				 -I$(top_srcdir)/src/modules/audio_conference_mixer/interface \
				 -I$(top_srcdir)/src/modules/audio_device/main/interface \
				 -I$(top_srcdir)/src/modules/audio_device/main/source \
				 -I$(top_srcdir)/src/modules/audio_processing/include \
				 -I$(top_srcdir)/src/modules/media_file/interface \
				 -I$(top_srcdir)/src/modules/rtp_rtcp/interface \
				 -I$(top_srcdir)/src/modules/udp_transport/interface \
				 -I$(top_srcdir)/src/modules/utility/interface \
				 -I$(top_srcdir)/src/system_wrappers/interface \
				 -I$(top_srcdir)/src \
				 -I$(top_srcdir)/src/test
voice_engine_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			      $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			      $(top_builddir)/src/voice_engine/main/libwebrtc_voice_engine.la \
			      $(top_builddir)/src/test/libtest.la

SUBDIRS = test
endif
