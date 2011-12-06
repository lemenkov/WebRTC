if WITH_TEST
TESTS =
noinst_PROGRAMS = $(TESTS) vie_auto_test

# Android-specific
# source/vie_autotest_android.cc

if WEBRTC_LINUX
linux_SOURCES = source/vie_autotest_linux.cc source/vie_window_manager_factory_linux.cc
endif

if WEBRTC_MAC
mac_SOURCES = source/vie_autotest_carbon_mac.cc \
	      source/vie_autotest_cocoa_mac.mm \
	      source/vie_window_manager_factory_mac.mm
endif

if WEBRTC_WINDOWS
win_SOURCES = source/vie_autotest_win.cc source/vie_window_manager_factory_win.cc
endif

vie_auto_test_SOURCES = automated/legacy_fixture.cc \
			automated/two_windows_fixture.cc \
			automated/vie_api_integration_test.cc \
			automated/vie_extended_integration_test.cc \
			automated/vie_rtp_fuzz_test.cc \
			automated/vie_standard_integration_test.cc \
			automated/vie_video_verification_test.cc \
			primitives/base_primitives.cc \
			primitives/codec_primitives.cc \
			primitives/framedrop_primitives.cc \
			primitives/framedrop_primitives_unittest.cc \
			primitives/general_primitives.cc \
			source/vie_autotest.cc \
			source/vie_autotest_base.cc \
			source/vie_autotest_capture.cc \
			source/vie_autotest_codec.cc \
			source/vie_autotest_custom_call.cc \
			source/vie_autotest_encryption.cc \
			source/vie_autotest_file.cc \
			source/vie_autotest_image_process.cc \
			source/vie_autotest_loopback.cc \
			source/vie_autotest_main.cc \
			source/vie_autotest_network.cc \
			source/vie_autotest_render.cc \
			source/vie_autotest_rtp_rtcp.cc \
			source/vie_autotest_simulcast.cc \
			source/vie_file_based_comparison_tests.cc \
			source/vie_window_creator.cc \
			$(linux_SOURCES) \
			$(mac_SOURCES) \
			$(win_SOURCES)

vie_auto_test_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			 @LIBX11_CXXFLAGS@ @LIBXEXT_CXXFLAGS@ \
			 -I./automated \
			 -I./interface \
			 -I./primitives \
			 -I$(top_srcdir)/src \
			 -I$(top_srcdir)/src/modules/video_capture/main/interface \
			 -I$(top_srcdir)/src/modules/video_render/main/interface \
			 -I$(top_srcdir)/src/system_wrappers/interface \
			 -I$(top_srcdir)/src/test \
			 -I$(top_srcdir)/src/voice_engine/main/interface \
			 -I$(top_srcdir)/src/video_engine \
			 -I$(top_srcdir)/src/video_engine/test/libvietest/include \
			 -I$(top_srcdir)/src/video_engine/include
vie_auto_test_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ @GFLAGS_LIBS@ @LIBX11_LIBS@ @LIBXEXT_LIBS@ \
		      $(top_builddir)/src/modules/video_capture/main/libwebrtc_video_capture.la \
		      $(top_builddir)/src/modules/video_render/main/libwebrtc_video_render.la \
		      $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
		      $(top_builddir)/src/video_engine/libwebrtc_video_engine.la \
		      $(top_builddir)/src/voice_engine/main/libwebrtc_voice_engine.la \
		      $(top_builddir)/src/video_engine/test/libvietest/libvietest.la \
		      $(top_builddir)/src/test/libtest/libtest.la \
		      $(top_builddir)/src/test/libtest.la \
		      $(top_builddir)/src/test/libmetrics.la
endif
