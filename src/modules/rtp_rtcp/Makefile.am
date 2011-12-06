lib_LTLIBRARIES = libwebrtc_rtp_rtcp.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/rtp_rtcp.h ./interface/rtp_rtcp_defines.h

libwebrtc_rtp_rtcp_la_SOURCES = \
				source/bitrate.cc \
				source/dtmf_queue.cc \
				source/forward_error_correction.cc \
				source/forward_error_correction_internal.cc \
				source/producer_fec.cc \
				source/receiver_fec.cc \
				source/rtcp_receiver.cc \
				source/rtcp_receiver_help.cc \
				source/rtcp_sender.cc \
				source/rtcp_utility.cc \
				source/rtp_format_vp8.cc \
				source/rtp_header_extension.cc \
				source/rtp_packet_history.cc \
				source/rtp_receiver.cc \
				source/rtp_receiver_audio.cc \
				source/rtp_receiver_video.cc \
				source/rtp_rtcp_impl.cc \
				source/rtp_sender.cc \
				source/rtp_sender_audio.cc \
				source/rtp_sender_video.cc \
				source/rtp_utility.cc \
				source/ssrc_database.cc \
				source/tmmbr_help.cc \
				source/transmission_bucket.cc \
				source/vp8_partition_aggregator.cc

libwebrtc_rtp_rtcp_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/system_wrappers/interface
libwebrtc_rtp_rtcp_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			       $(top_builddir)/src/modules/remote_bitrate_estimator/libwebrtc_remote_bitrate_estimator.la
libwebrtc_rtp_rtcp_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
common_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
		  -I$(top_srcdir)/src/system_wrappers/interface \
		  -I$(top_srcdir)/src -I./source
common_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
	       $(top_builddir)/src/modules/rtp_rtcp/libwebrtc_rtp_rtcp.la \
	       $(top_builddir)/src/modules/remote_bitrate_estimator/libwebrtc_remote_bitrate_estimator.la \
	       $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
	       $(top_builddir)/test/libtest.la

TESTS = rtp_rtcp_unittest
noinst_PROGRAMS = $(TESTS) test_fec

rtp_rtcp_unittest_SOURCES = source/fec_test_helper.cc \
			    source/producer_fec_unittest.cc \
			    source/receiver_fec_unittest.cc \
			    source/rtcp_format_remb_unittest.cc \
			    source/rtp_fec_unittest.cc \
			    source/rtp_format_vp8_test_helper.cc \
			    source/rtp_format_vp8_unittest.cc \
			    source/rtp_packet_history_unittest.cc \
			    source/rtp_utility_unittest.cc \
			    source/rtp_header_extension_unittest.cc \
			    source/rtp_sender_unittest.cc \
			    source/rtcp_sender_unittest.cc \
			    source/rtcp_receiver_unittest.cc \
			    source/transmission_bucket_unittest.cc \
			    source/vp8_partition_aggregator_unittest.cc
rtp_rtcp_unittest_CXXFLAGS = $(common_CXXFLAGS)
rtp_rtcp_unittest_LDADD = $(common_LDADD)

# FIXME
#test_api_SOURCES = test/testAPI/test_api.cc test/testAPI/test_api_audio.cc test/testAPI/test_api_nack.cc test/testAPI/test_api_rtcp.cc test/testAPI/test_api_video.cc
#test_api_CXXFLAGS = $(common_CXXFLAGS)
#test_api_LDADD = $(common_LDADD)

test_fec_SOURCES = test/testFec/test_fec.cc
test_fec_CXXFLAGS = $(common_CXXFLAGS) -I$(top_srcdir)/test
test_fec_LDADD = $(common_LDADD)

# win-only
#test_bitstream_SOURCES = test/bitstreamTest/bitstreamTest.cc
#test_bitstream_CXXFLAGS = $(common_CXXFLAGS)
#test_bitstream_LDADD = $(common_LDADD)
#test_h263_parser_SOURCES = test/testH263Parser/testH263Parser.cc
#test_h263_parser_CXXFLAGS = $(common_CXXFLAGS)
#test_h263_parser_LDADD = $(common_LDADD)
#test_rate_control_SOURCES = test/testRateControl/testRateControl.cc
#test_rate_control_CXXFLAGS = $(common_CXXFLAGS)
#test_rate_control_LDADD = $(common_LDADD)
#test_tmmbr_SOURCES = test/testTMMBR/testTMMBR.cc
#test_tmmbr_CXXFLAGS = $(common_CXXFLAGS)
#test_tmmbr_LDADD = $(common_LDADD)

#test_bwe_SOURCES = test/test_bwe/unit_test.cc
#test_bwe_CXXFLAGS = $(common_CXXFLAGS)
#test_bwe_LDADD = $(common_LDADD)

endif
