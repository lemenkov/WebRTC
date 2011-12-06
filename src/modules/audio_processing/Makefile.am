SUBDIRS = utility ns aec aecm agc
lib_LTLIBRARIES = libwebrtc_audio_processing.la

if NS_FIXED
DEFS += -DWEBRTC_NS_FIXED
else
DEFS += -DWEBRTC_NS_FLOAT
endif

if WEBRTC_PROTOBUF
DEFS += -DWEBRTC_AUDIOPROC_DEBUG_DUMP
protobuf_SRC = debug.pb.cc
endif

# Targets for generating protocol buffer code.
%.pb.cc %.pb.h: %.proto
	protoc -I$(srcdir) --cpp_out=. $^

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = include/audio_processing.h \
			aec/include/echo_cancellation.h \
			aecm/include/echo_control_mobile.h \
			agc/include/gain_control.h \
			ns/include/noise_suppression.h ns/include/noise_suppression_x.h

libwebrtc_audio_processing_la_SOURCES = $(protobuf_SRC) \
					audio_buffer.cc \
					audio_processing_impl.cc \
					echo_cancellation_impl.cc \
					echo_control_mobile_impl.cc \
					gain_control_impl.cc \
					high_pass_filter_impl.cc \
					level_estimator_impl.cc \
					noise_suppression_impl.cc \
					splitting_filter.cc \
					processing_component.cc \
					voice_detection_impl.cc

libwebrtc_audio_processing_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
					 @PROTOBUF_CXXFLAGS@ \
					 -I$(top_srcdir)/src/common_audio/signal_processing/include \
					 -I$(top_srcdir)/src/common_audio/vad/include \
					 -I$(top_srcdir)/src/system_wrappers/interface \
					 -I$(top_srcdir)/src/modules/audio_processing/utility \
					 -I$(top_srcdir)/src/modules/audio_processing/ns/include \
					 -I$(top_srcdir)/src/modules/audio_processing/aec/include \
					 -I$(top_srcdir)/src/modules/audio_processing/aecm/include \
					 -I$(top_srcdir)/src/modules/audio_processing/agc/include

libwebrtc_audio_processing_la_LIBADD = @PROTOBUF_LIBS@ \
				       $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
				       $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la \
				       $(top_builddir)/src/common_audio/vad/libwebrtc_vad.la \
				       $(top_builddir)/src/modules/audio_processing/utility/libapm_util.la \
				       $(top_builddir)/src/modules/audio_processing/ns/libns.la \
				       $(top_builddir)/src/modules/audio_processing/aec/libaec.la \
				       $(top_builddir)/src/modules/audio_processing/aecm/libaecm.la \
				       $(top_builddir)/src/modules/audio_processing/agc/libagc.la

libwebrtc_audio_processing_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
if WEBRTC_PROTOBUF
# Protobuf is required for tests

if NS_FIXED
DEFS += -DWEBRTC_AUDIOPROC_FIXED_PROFILE
else
DEFS += -DWEBRTC_AUDIOPROC_FLOAT_PROFILE
endif

protobuf_test_SRC = test/unittest.pb.cc

common_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
		  -I$(top_srcdir)/src/common_audio/signal_processing/include \
		  -I$(top_srcdir)/src/system_wrappers/interface \
		  -I$(top_srcdir)/test
common_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
	       $(top_builddir)/src/modules/audio_processing/libwebrtc_audio_processing.la \
	       $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
	       $(top_builddir)/test/libtest.la

TESTS = audio_processing_unittest
noinst_PROGRAMS = $(TESTS) process_test unpack

audio_processing_unittest_SOURCES = $(protobuf_test_SRC) test/unit_test.cc
audio_processing_unittest_CXXFLAGS = $(common_CXXFLAGS)
audio_processing_unittest_LDADD = $(common_LDADD) @PROTOBUF_LIBS@

process_test_SOURCES = test/process_test.cc
process_test_CXXFLAGS = $(common_CXXFLAGS)
process_test_LDADD = $(common_LDADD)

unpack_SOURCES = test/unpack.cc
unpack_CXXFLAGS = $(common_CXXFLAGS)
unpack_LDADD = $(common_LDADD) @GFLAGS_LIBS@
endif
endif

CLEANFILES = debug.pb.cc debug.pb.h test/unittest.pb.cc test/unittest.pb.h
