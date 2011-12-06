lib_LTLIBRARIES = libwebrtc_udp_transport.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./interface/udp_transport.h

if WEBRTC_POSIX
posix_SRCS = \
				     source/udp_socket_manager_posix.cc \
				     source/udp_socket_posix.cc
endif

if WEBRTC_WINDOWS
win_SRCS = \
				     source/traffic_control_windows.cc \
				     source/udp_socket2_manager_windows.cc \
				     source/udp_socket2_windows.cc
endif
libwebrtc_udp_transport_la_SOURCES = \
				     source/udp_socket_manager_wrapper.cc \
				     source/udp_socket_wrapper.cc \
				     source/udp_transport_impl.cc \
				     $(posix_SRCS) \
				     $(win_SRCS)

libwebrtc_udp_transport_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
			    -I$(top_srcdir)/src/system_wrappers/interface

libwebrtc_udp_transport_la_LIBADD = $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la

libwebrtc_udp_transport_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = udp_transport_unittest
noinst_PROGRAMS = $(TESTS)
udp_transport_unittest_SOURCES = \
				 source/udp_socket_manager_unittest.cc \
				 source/udp_socket_wrapper_unittest.cc \
				 source/udp_transport_unittest.cc
udp_transport_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
				  -I$(top_srcdir)/src/system_wrappers/interface \
				  -I$(top_srcdir) \
				  -I$(top_srcdir)/src -I$(top_srcdir)/test -I./source
udp_transport_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/udp_transport/libwebrtc_udp_transport.la \
			   $(top_builddir)/test/libtest.la

if FALSE
# TODO
socket_manager_test_SOURCES = test/SocketManagerTest.cc
socket_manager_test_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ \
			       -I$(top_srcdir)/src -I$(top_srcdir)/test -I./source \
			       -I$(top_srcdir)/src/system_wrappers/interface
socket_manager_test_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/modules/udp_transport/libwebrtc_udp_transport.la \
			   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			   $(top_builddir)/test/libtest.la
endif
endif
