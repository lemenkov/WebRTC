lib_LTLIBRARIES = libwebrtc_system_wrappers.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = \
			./interface/aligned_malloc.h \
			./interface/atomic32_wrapper.h \
			./interface/condition_variable_wrapper.h \
			./interface/constructor_magic.h \
			./interface/cpu_features_wrapper.h \
			./interface/cpu_info.h \
			./interface/cpu_wrapper.h \
			./interface/critical_section_wrapper.h \
			./interface/data_log.h \
			./interface/data_log_c.h \
			./interface/data_log_impl.h \
			./interface/event_wrapper.h \
			./interface/file_wrapper.h \
			./interface/fix_interlocked_exchange_pointer_win.h \
			./interface/list_wrapper.h \
			./interface/map_wrapper.h \
			./interface/ref_count.h \
			./interface/rw_lock_wrapper.h \
			./interface/scoped_ptr.h \
			./interface/scoped_refptr.h \
			./interface/sort.h \
			./interface/static_instance.h \
			./interface/thread_wrapper.h \
			./interface/tick_util.h \
			./interface/trace.h

##
## OS features
##

if WEBRTC_LINUX
libsystem_wrappers_linux_la_SOURCES = \
				source/cpu_linux.cc
linux_RT = -lrt
endif

if WEBRTC_MAC
libsystem_wrappers_mac_la_SOURCES = \
				source/cpu_mac.cc
mac_RT =
endif

if WEBRTC_POSIX
libsystem_wrappers_posix_la_SOURCES = \
				source/condition_variable_posix.cc \
				source/critical_section_posix.cc \
				source/event_posix.cc \
				source/rw_lock_posix.cc \
				source/thread_posix.cc \
				source/trace_posix.cc
endif

if WEBRTC_WINDOWS
libsystem_wrappers_win_la_SOURCES = \
				source/condition_variable_win.cc \
				source/cpu_win.cc \
				source/critical_section_win.cc \
				source/event_win.cc \
				source/rw_lock_win.cc \
				source/thread_win.cc \
				source/trace_win.cc
endif

##
## Additional features
##

##
## Common settings
##

if WEBRTC_LOGGING
libsystem_wrappers_logger_la_SOURCES = \
				source/data_log.cc
else
libsystem_wrappers_logger_la_SOURCES = \
				source/data_log_no_op.cc
endif

# For Android only
# source/cpu_features_arm.c

# Disabled for now
# source/list_stl.cc
# source/map_no_stl.cc
# source/rw_lock_generic.cc

# For Chromium
# source/cpu_no_op.cc
# source/trace_impl_no_op.cc

libwebrtc_system_wrappers_la_SOURCES = \
				source/aligned_malloc.cc \
				source/atomic32.cc \
				source/condition_variable.cc \
				source/cpu.cc \
				source/cpu_features.cc \
				source/cpu_info.cc \
				source/critical_section.cc \
				source/data_log_c.cc \
				$(libsystem_wrappers_logger_la_SOURCES) \
				source/event.cc \
				source/file_impl.cc \
				source/list_no_stl.cc \
				source/map.cc \
				source/rw_lock.cc \
				source/sort.cc \
				source/thread.cc \
				source/trace_impl.cc \
				$(libsystem_wrappers_linux_la_SOURCES) \
				$(libsystem_wrappers_mac_la_SOURCES) \
				$(libsystem_wrappers_posix_la_SOURCES) \
				$(libsystem_wrappers_win_la_SOURCES)

# This assumes that we want the POSIX implementation -- should eventually be
# converted to a conditional to include Windows support
libwebrtc_system_wrappers_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) \
				 -I$(srcdir)/interface -I./source/spreadsortlib
libwebrtc_system_wrappers_la_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) \
				 -I$(srcdir)/interface -I./source/spreadsortlib
libwebrtc_system_wrappers_la_LIBADD = $(linux_RT) $(mac_RT)
libwebrtc_system_wrappers_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)


if WITH_TEST
TESTS = system_wrappers_unittest
noinst_PROGRAMS = $(TESTS)
if WEBRTC_LOGGING
logger_unittest_SOURCES = source/data_log_unittest.cc
else
logger_unittest_SOURCES = source/data_log_unittest_disabled.cc
endif
system_wrappers_unittest_SOURCES = \
				   source/cpu_measurement_harness.cc \
				   source/cpu_measurement_harness.h \
				   source/cpu_wrapper_unittest.cc \
				   source/data_log_c_helpers_unittest.h \
				   source/data_log_c_helpers_unittest.c \
				   source/data_log_helpers_unittest.cc \
				   source/list_unittest.cc \
				   source/map_unittest.cc \
				   source/trace_unittest.cc \
				   $(logger_unittest_SOURCES)
system_wrappers_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ -I$(top_srcdir)/src -I$(top_srcdir)/test -I./source
system_wrappers_unittest_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ -I$(top_srcdir)/src -I$(top_srcdir)/test -I./source
system_wrappers_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/system_wrappers/libwebrtc_system_wrappers.la \
			   $(top_builddir)/test/libtest.la
endif
