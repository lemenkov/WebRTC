if WITH_TEST
noinst_LTLIBRARIES = libvietest.la
libvietest_la_SOURCES = helpers/vie_fake_camera.cc \
			helpers/vie_file_capture_device.cc \
			helpers/vie_to_file_renderer.cc \
			testbed/tb_I420_codec.cc \
			testbed/tb_capture_device.cc \
			testbed/tb_external_transport.cc \
			testbed/tb_interfaces.cc \
			testbed/tb_video_channel.cc

libvietest_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
		    -I./include \
		    -I$(top_srcdir)/test \
		    -I$(top_srcdir)/src \
		    -I$(top_srcdir)/src/system_wrappers/interface \
		    -I$(top_srcdir)/src/video_engine/include
endif
