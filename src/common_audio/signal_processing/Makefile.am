lib_LTLIBRARIES = libwebrtc_signal_processing.la

webrtcincludedir = $(includedir)/webrtc
webrtcinclude_HEADERS = ./include/signal_processing_library.h ./include/spl_inl.h

# Android-specific

# if WEBRTC_ARCH_ARM_V7A
# ./include/spl_inl_armv7.h
# fi

# if ARCH_ARM_HAVE_NEON
# cross_correlation_neon.s
# downsample_fast_neon.s
# min_max_operations_neon.s
# vector_scaling_operations_neon.s
# else
# cross_correlation.c
# downsample_fast.c
# fi

# if ARCH_ARM_HAVE_ARMV7A
# filter_ar_fast_q12_armv7.s
# else
# filter_ar_fast_q12.c
# fi

# TARGET_ARCH == arm
# complex_bit_reverse_arm.s
# spl_sqrt_floor.s
# else
# complex_bit_reverse.c
# spl_sqrt_floor.c
# fi

# Not used at all
# webrtc_fft_t_1024_8.c
# webrtc_fft_t_rad.c

libwebrtc_signal_processing_la_SOURCES = auto_corr_to_refl_coef.c \
		    auto_correlation.c \
		    complex_bit_reverse.c \
		    complex_fft.c \
		    copy_set_operations.c \
		    cross_correlation.c \
		    division_operations.c \
		    dot_product_with_scale.c \
		    downsample_fast.c \
		    energy.c \
		    filter_ar.c \
		    filter_ar_fast_q12.c \
		    filter_ma_fast_q12.c \
		    get_hanning_window.c \
		    get_scaling_square.c \
		    ilbc_specific_functions.c \
		    levinson_durbin.c \
		    lpc_to_refl_coef.c \
		    min_max_operations.c \
		    randomization_functions.c \
		    refl_coef_to_lpc.c \
		    resample.c \
		    resample_48khz.c \
		    resample_by_2.c \
		    resample_by_2_internal.c \
		    resample_fractional.c \
		    spl_sqrt.c \
		    spl_sqrt_floor.c \
		    spl_version.c \
		    splitting_filter.c \
		    sqrt_of_one_minus_x_squared.c \
		    vector_scaling_operations.c

libwebrtc_signal_processing_la_CFLAGS = $(AM_CFLAGS) $(COMMON_CFLAGS)
libwebrtc_signal_processing_la_LIBADD =
libwebrtc_signal_processing_la_LDFLAGS = $(AM_LDFLAGS) -version-info $(WEBRTC_VERSION_INFO)

if WITH_TEST
TESTS = signal_processing_unittest
noinst_PROGRAMS = $(TESTS)
signal_processing_unittest_SOURCES = signal_processing_unittest.cc
signal_processing_unittest_CXXFLAGS = $(AM_CXXFLAGS) $(COMMON_CXXFLAGS) @GTEST_CXXFLAGS@ @GMOCK_CXXFLAGS@ -I$(top_srcdir)/src/common_audio/signal_processing/include -I$(top_srcdir)
signal_processing_unittest_LDADD = @GTEST_LIBS@ @GMOCK_LIBS@ \
			   $(top_builddir)/src/common_audio/signal_processing/libwebrtc_signal_processing.la \
			   $(top_builddir)/src/test/libtest.la
endif
