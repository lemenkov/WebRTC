if WITH_TEST
TESTS =
noinst_PROGRAMS = $(TESTS) voe_auto_test
voe_auto_test_SOURCES = automated_mode.cc \
			extended/agc_config_test.cc \
			extended/ec_metrics_test.cc \
			fakes/fake_external_transport.cc \
			fixtures/after_initialization_fixture.cc \
			fixtures/after_streaming_fixture.cc \
			fixtures/before_initialization_fixture.cc \
			fuzz/rtp_fuzz_test.cc \
			resource_manager.cc \
			standard/audio_processing_test.cc \
			standard/call_report_test.cc \
			standard/codec_before_streaming_test.cc \
			standard/codec_test.cc \
			standard/dtmf_test.cc \
			standard/encryption_test.cc \
			standard/external_media_test.cc \
			standard/file_before_streaming_test.cc \
			standard/file_test.cc \
			standard/hardware_before_initializing_test.cc \
			standard/hardware_before_streaming_test.cc \
			standard/hardware_test.cc \
			standard/manual_hold_test.cc \
			standard/mixing_test.cc \
			standard/neteq_stats_test.cc \
			standard/neteq_test.cc \
			standard/network_before_streaming_test.cc \
			standard/network_test.cc \
			standard/rtp_rtcp_before_streaming_test.cc \
			standard/rtp_rtcp_test.cc \
			standard/video_sync_test.cc \
			standard/voe_base_misc_test.cc \
			standard/volume_test.cc \
			voe_cpu_test.cc \
			voe_extended_test.cc \
			voe_standard_test.cc \
			voe_stress_test.cc \
			voe_unit_test.cc
voe_auto_test_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			 -I./fixtures \
			 -I$(top_srcdir) \
			 -I$(top_srcdir)/src \
			 -I$(top_srcdir)/src/modules/audio_device/main/interface \
			 -I$(top_srcdir)/src/system_wrappers/interface \
			 -I$(top_srcdir)/src/test \
			 -I$(top_srcdir)/src/voice_engine/main/source \
			 -I$(top_srcdir)/src/voice_engine/main/interface
voe_auto_test_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
		      $(top_builddir)/src/modules/audio_device/main/libwebrtc_audio_device.la \
		      $(top_builddir)/src/voice_engine/main/libwebrtc_voice_engine.la \
		      $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
		      $(top_builddir)/src/test/libtest/libtest.la \
		      $(top_builddir)/src/test/libtest.la
endif
