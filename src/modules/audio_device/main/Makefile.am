lib_LTLIBRARIES = libwebrtc_audio_device.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/audio_device.h ./interface/audio_device_defines.h

# FIXME allow dummy devices

if WEBRTC_LINUX
linux_INCLUDES = -I./source/linux
linux_SOURCES = \
		source/linux/audio_device_utility_linux.cc \
		source/linux/latebindingsymboltable_linux.cc
if WEBRTC_LINUX_ALSA
linux_alsa_SOURCES = \
		source/linux/alsasymboltable_linux.cc \
		source/linux/audio_device_alsa_linux.cc \
		source/linux/audio_mixer_manager_alsa_linux.cc
DEFS += -DLINUX_ALSA
endif
if WEBRTC_LINUX_PULSE
linux_pulse_SOURCES = \
		source/linux/audio_device_pulse_linux.cc \
		source/linux/audio_mixer_manager_pulse_linux.cc \
		source/linux/pulseaudiosymboltable_linux.cc
DEFS += -DLINUX_PULSE
endif
endif

if WEBRTC_MAC
mac_INCLUDES = -I./source/mac
mac_SOURCES = \
	      source/mac/audio_device_mac.cc \
	      source/mac/audio_device_utility_mac.cc \
	      source/mac/audio_mixer_manager_mac.cc
endif

if WEBRTC_WINDOWS
windows_INCLUDES = -I./source/win
windows_SOURCES = \
		  source/win/audio_device_core_win.cc \
		  source/win/audio_device_utility_win.cc \
		  source/win/audio_device_wave_win.cc \
		  source/win/audio_mixer_manager_win.cc
endif

libwebrtc_audio_device_la_SOURCES = \
				    source/audio_device_buffer.cc \
				    source/audio_device_generic.cc \
				    source/audio_device_impl.cc \
				    source/audio_device_utility.cc \
				    source/dummy/audio_device_dummy.cc \
				    source/dummy/audio_device_utility_dummy.cc \
				    $(mac_SOURCES) \
				    $(linux_SOURCES) \
				    $(linux_alsa_SOURCES) \
				    $(linux_pulse_SOURCES) \
				    $(windows_SOURCES)

libwebrtc_audio_device_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/system_wrappers/interface \
			    -I$(top_srcdir)/src/common_audio/resampler/include \
			    -I$(top_srcdir)/src/common_audio/signal_processing/include \
			    -I ./source -I./source/dummy \
			    $(linux_INCLUDES) $(LIBALSA_CFLAGS) $(LIBPULSE_CFLAGS) \
			    $(mac_INCLUDES) \
			    $(windows_INCLUDES)

libwebrtc_audio_device_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
				   $(top_builddir)/src/common_audio/resampler/libwebrtc_resampler.la \
				   $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la \
				   $(LIBALSA_LIBS) $(LIBPULSE_LIBS)

libwebrtc_audio_device_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
common_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
		  -I$(top_srcdir)/test -I./source \
		  -I$(top_srcdir)/src/system_wrappers/interface \
		  -I$(top_srcdir)/src/common_audio/resampler/include \
		  -I$(top_srcdir)/src/modules/utility/interface
common_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
	       $(top_builddir)/src/modules/audio_device/main/libwebrtc_audio_device.la \
	       $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
	       $(top_builddir)/src/common_audio/resampler/libwebrtc_resampler.la \
	       $(top_builddir)/src/modules/utility/libwebrtc_utility.la \
	       $(top_builddir)/test/libtest.la

# API tests are only available for PulseAudio
#TESTS = audio_device_test_api audio_device_test_func
TESTS = audio_device_test_func

#noinst_PROGRAMS = $(TESTS)
noinst_PROGRAMS = audio_device_test_api audio_device_test_func

audio_device_test_api_SOURCES = test/audio_device_test_api.cc
audio_device_test_api_CXXFLAGS = $(common_CXXFLAGS)
audio_device_test_api_LDADD = $(common_LDADD)

audio_device_test_func_SOURCES = test/func_test_manager.cc
audio_device_test_func_CXXFLAGS = $(common_CXXFLAGS)
audio_device_test_func_LDADD = $(common_LDADD)
endif
