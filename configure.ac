AC_INIT([webrtc], [0], [http://groups.google.com/group/discuss-webrtc], [webrtc], [http://www.webrtc.org/])

AC_CANONICAL_TARGET

AM_INIT_AUTOMAKE([dist-bzip2 no-dist-gzip tar-ustar foreign])

AC_SUBST(WEBRTC_VERSION_INFO, [0:0:0])

AC_PROG_CC
AC_PROG_CXX
AC_PROG_LIBTOOL
AC_PROG_INSTALL

AC_LANG_C
AC_LANG_CPLUSPLUS

case "$target_os" in
	linux*)
		linux="yes"
		posix="yes"
		CFLAGS="$CFLAGS -DWEBRTC_LINUX -DWEBRTC_POSIX -DWEBRTC_THREAD_RR"
		CXXFLAGS="$CXXFLAGS -DWEBRTC_LINUX -DWEBRTC_POSIX -DWEBRTC_THREAD_RR"
		;;
	darwin*)
		macosx="yes"
		posix="yes"
		CFLAGS="$CFLAGS -DWEBRTC_MAC -DWEBRTC_POSIX -DWEBRTC_THREAD_RR -DWEBRTC_CLOCK_TYPE_REALTIME"
		CXXFLAGS="$CXXFLAGS -DWEBRTC_MAC -DWEBRTC_POSIX -DWEBRTC_THREAD_RR -DWEBRTC_CLOCK_TYPE_REALTIME"
		;;
	mingw*)
		# FIXME
		windows="yes"
		CFLAGS="$CFLAGS -D_WIN32"
		CXXFLAGS="$CXXFLAGS -D_WIN32"
		;;
esac

# Check for CPU-specific features
case "$target_cpu" in
	i786|x86_64)
		has_sse2="yes"
		has_neon="no"
		;;
	arm*)
		has_sse2="no"
		AC_ARG_ENABLE(neon,
			      [  --enable-neon           enable ARM NEON support],
			      [
			       AC_MSG_CHECKING(for NEON in current arch/CFLAGS)
			       AC_LINK_IFELSE([
					       AC_LANG_PROGRAM(
							       [[
								#include <arm_neon.h>
								int32x4_t testfunc(int16_t *a, int16_t *b)
								{
									return vmull_s16(vld1_s16(a), vld1_s16(b));
								}
								]]
							       )
					       ],
					       [has_neon="yes"],
					       [has_neon="no"]
					      )
			       AC_MSG_RESULT($has_neon)
			      ]
			     )
		;;
	*)
		has_sse2="no"
		has_neon="no"
		;;
esac

AC_ARG_WITH([ns-mode],
	    AC_HELP_STRING([--with-ns-mode=float|fixed], [Noise suppresion mode to use. Default is float]))

case "${with_ns_mode}" in
	"fixed")
		NS_FIXED=1
		;;
	*)
		NS_FIXED=0
		;;
esac

AC_ARG_WITH([logging],
	    AC_HELP_STRING([--with-logging],[enable logging.]),
	    [logging="$withval"],[logging="no"])

AC_CHECK_HEADER([libyuv.h],,[AC_MSG_ERROR([libyuv.h header not found])])
AC_CHECK_LIB(
	     [yuv],
	     [RGB24ToI420],
	     [
	      LIBYUV_LIBS="-lyuv"
	      AC_SUBST([LIBYUV_LIBS])
	     ],
	     [AC_MSG_ERROR([libyuv library missing])]
	    )

AC_CHECK_HEADER([jpeglib.h],,[AC_MSG_ERROR([jpeglib.h header not found])])
AC_CHECK_LIB(
	     [jpeg],
	     [jpeg_destroy_decompress],
	     [
	      LIBJPEG_LIBS="-ljpeg"
	      AC_SUBST([LIBJPEG_LIBS])
	     ],
	     [AC_MSG_ERROR([libjpeg library missing])]
	    )

AC_C_BIGENDIAN(
	       [
		CFLAGS="$CFLAGS -DWEBRTC_BIG_ENDIAN"
		CXXFLAGS="$CXXFLAGS -DWEBRTC_BIG_ENDIAN"
		],
	       ,
	       [AC_MSG_ERROR([Unknown endianness])],
	       [AC_MSG_ERROR([No support for universal binaries yet])]
	       )

AM_CONDITIONAL(NS_FIXED, [test "x${NS_FIXED}" = "x1"])

AC_ARG_WITH(
	    [test],
	    AC_HELP_STRING([--with-test],[enable test suite.]),
	    [with_test="$withval"],
	    [with_test="no"]
	   )

##
## Audio codecs
##

AC_ARG_WITH([audiocodec-amr],
	    AC_HELP_STRING([--with-audiocodec-amr],[enable AMR audiocodec.]),
	    [audiocodec_amr="$withval"],[audiocodec_amr="no"])
AC_ARG_WITH([audiocodec-amrwb],
	    AC_HELP_STRING([--with-audiocodec-amrwb],[enable AMR-WB audiocodec.]),
	    [audiocodec_amrwb="$withval"],[audiocodec_amrwb="no"])
AC_ARG_WITH([audiocodec-avt],
	    AC_HELP_STRING([--with-audiocodec-avt],[enable DTMF audio payload.]),
	    [audiocodec_avt="$withval"],[audiocodec_avt="yes"])
AC_ARG_WITH([audiocodec-celt],
	    AC_HELP_STRING([--with-audiocodec-celt],[enable CELT audiocodec.]),
	    [audiocodec_celt="$withval"],[audiocodec_celt="no"])
AC_ARG_WITH([audiocodec-g722],
	    AC_HELP_STRING([--with-audiocodec-g722],[enable G.722 audiocodec.]),
	    [audiocodec_g722="$withval"],[audiocodec_g722="yes"])
AC_ARG_WITH([audiocodec-g7221],
	    AC_HELP_STRING([--with-audiocodec-g7221],[enable G.722.1 audiocodec.]),
	    [audiocodec_g7221="$withval"],[audiocodec_g7221="no"])
AC_ARG_WITH([audiocodec-g7221c],
	    AC_HELP_STRING([--with-audiocodec-g7221c],[enable G.722.1C audiocodec.]),
	    [audiocodec_g7221c="$withval"],[audiocodec_g7221c="no"])
AC_ARG_WITH([audiocodec-g729],
	    AC_HELP_STRING([--with-audiocodec-g729],[enable G.729 audiocodec.]),
	    [audiocodec_g729="$withval"],[audiocodec_g729="no"])
AC_ARG_WITH([audiocodec-g7291],
	    AC_HELP_STRING([--with-audiocodec-g7291],[enable G.729.1 audiocodec.]),
	    [audiocodec_g7291="$withval"],[audiocodec_g7291="no"])
AC_ARG_WITH([audiocodec-gsmfr],
	    AC_HELP_STRING([--with-audiocodec-gsmfr],[enable GSM (Full Rate a.k.a 06.10) audiocodec.]),
	    [audiocodec_gsmfr="$withval"],[audiocodec_gsmfr="no"])
AC_ARG_WITH([audiocodec-ilbc],
	    AC_HELP_STRING([--with-audiocodec-ilbc],[enable iLBC audiocodec.]),
	    [audiocodec_ilbc="$withval"],[audiocodec_ilbc="yes"])
AC_ARG_WITH([audiocodec-isac],
	    AC_HELP_STRING([--with-audiocodec-isac],[enable ISAC audiocodec.]),
	    [audiocodec_isac="$withval"],[audiocodec_isac="yes"])
AC_ARG_WITH([audiocodec-isacfx],
	    AC_HELP_STRING([--with-audiocodec-isacfx],[enable iSAC fixed point audiocodec (instead of iSAC).]),
	    [audiocodec_isacfx="$withval"],[audiocodec_isacfx="no"])
AC_ARG_WITH([audiocodec-opus],
	    AC_HELP_STRING([--with-audiocodec-opus],[enable OPUS audiocodec.]),
	    [audiocodec_opus="$withval"],[audiocodec_opus="no"])
AC_ARG_WITH([audiocodec-pcm16b],
	    AC_HELP_STRING([--with-audiocodec-pcm16b],[enable PCM (uncompressed) audiocodec.]),
	    [audiocodec_pcm16b="$withval"],[audiocodec_pcm16b="yes"])
AC_ARG_WITH([audiocodec-red],
	    AC_HELP_STRING([--with-audiocodec-red],[enable redundant audio payload.]),
	    [audiocodec_red="$withval"],[audiocodec_red="yes"])
AC_ARG_WITH([audiocodec-speex],
	    AC_HELP_STRING([--with-audiocodec-speex],[enable SPEEX audiocodec.]),
	    [audiocodec_speex="$withval"],[audiocodec_speex="no"])

if test "$audiocodec_amr" = "yes" ; then WRT_LIB_AMR="-lwebrtc_codecs_amr" ; fi
if test "$audiocodec_amrwb" = "yes" ; then WRT_LIB_AMRWB="-lwebrtc_codecs_amrwb" ; fi
# No specific library for AVT codec, so no substitution. Continue to CELT
if test "$audiocodec_celt" = "yes" ; then WRT_LIB_CELT="-lwebrtc_codecs_celt" ; fi
if test "$audiocodec_g722" = "yes" ; then WRT_LIB_G722="-lwebrtc_codecs_g722" ; fi
if test "$audiocodec_g7221" = "yes" ; then WRT_LIB_G7221="-lwebrtc_codecs_g7221" ; fi
if test "$audiocodec_g7221c" = "yes" ; then WRT_LIB_G7221C="-lwebrtc_codecs_g7221c" ; fi
if test "$audiocodec_g729" = "yes" ; then WRT_LIB_G729="-lwebrtc_codecs_g729" ; fi
if test "$audiocodec_g7291" = "yes" ; then WRT_LIB_G7291="-lwebrtc_codecs_g7291" ; fi
if test "$audiocodec_gsmfr" = "yes" ; then WRT_LIB_GSMFR="-lwebrtc_codecs_gcmfr" ; fi
if test "$audiocodec_ilbc" = "yes" ; then WRT_LIB_ILBC="-lwebrtc_codecs_ilbc" ; fi
if test "$audiocodec_isac" = "yes" ; then WRT_LIB_ISAC="-lwebrtc_codecs_isac" ; fi
if test "$audiocodec_isacfx" = "yes" ; then WRT_LIB_ISACFX="-lwebrtc_codecs_isac" ; fi
if test "$audiocodec_opus" = "yes" ; then WRT_LIB_OPUS="-lwebrtc_codecs_opus" ; fi
if test "$audiocodec_pcm16b" = "yes" ; then WRT_LIB_PCM16B="-lwebrtc_codecs_pcm16b" ; fi
# No specific library for RED codec, so no substitution. Continue to SPEEX
if test "$audiocodec_speex" = "yes" ; then WRT_LIB_SPEEX="-lwebrtc_codecs_speex" ; fi

AC_SUBST([WRT_LIB_AMR])
AC_SUBST([WRT_LIB_AMRWB])
AC_SUBST([WRT_LIB_CELT])
AC_SUBST([WRT_LIB_G722])
AC_SUBST([WRT_LIB_G7221])
AC_SUBST([WRT_LIB_G7221C])
AC_SUBST([WRT_LIB_G729])
AC_SUBST([WRT_LIB_G7291])
AC_SUBST([WRT_LIB_GSMFR])
AC_SUBST([WRT_LIB_ILBC])
AC_SUBST([WRT_LIB_ISAC])
AC_SUBST([WRT_LIB_ISACFX])
AC_SUBST([WRT_LIB_OPUS])
AC_SUBST([WRT_LIB_PCM16B])
AC_SUBST([WRT_LIB_SPEEX])

##
## Video codecs
##

AC_ARG_WITH([videocodec-i420],
	    AC_HELP_STRING([--with-videocodec-i420],[enable I420 videocodec.]),
	    [videocodec_i420="$withval"],[videocodec_i420="yes"])
AC_ARG_WITH([videocodec-vp8],
	    AC_HELP_STRING([--with-videocodec-vp8],[enable VP8 videocodec.]),
	    [videocodec_vp8="$withval"],[videocodec_vp8="yes"])

if test "$videocodec_vp8" = "yes" ; then
AC_CHECK_LIB([vpx],
	     [vpx_codec_vp8_cx],
	     [
	      LIBVPX_CFLAGS=`pkg-config vpx --cflags`
	      LIBVPX_CXXFLAGS=`pkg-config vpx --cflags`
	      LIBVPX_LIBS=`pkg-config vpx --libs`
	      LIBVPX_MODVERSION=`pkg-config --modversion vpx`
	      if test "$LIBVPX_MODVERSION" = "1.0.0" ; then
		      AC_MSG_WARN([Found libvpx ver. 1.0.0])
		      LIBVPX_VERSION="971"
	      else
		      if test "$LIBVPX_MODVERSION" = "0.9.6" ; then
			      AC_MSG_WARN([Found libvpx ver. 0.9.6])
			      LIBVPX_VERSION="960"
		      else
			      if test "$LIBVPX_MODVERSION" = "0.9.1" ; then
				      # RHEL/EPEL issue
				      AC_MSG_WARN([Found libvpx ver. 0.9.6 (wrong pkg-config info in EPEL)])
				      LIBVPX_VERSION="960"
			      else
				      AC_MSG_ERROR([Unknown/untested libvpx version])
			fi
		fi
	      fi
	      AC_SUBST([LIBVPX_CFLAGS])
	      AC_SUBST([LIBVPX_CXXFLAGS])
	      AC_SUBST([LIBVPX_LIBS])
	      AC_SUBST([LIBVPX_VERSION])
	     ],
	     [AC_MSG_ERROR([libvpx library missing])]
	    )
else
	LIBVPX_VERSION="n/a"
fi

if test "$videocodec_i420" = "yes" ; then WRT_LIB_I420="-lwebrtc_codecs_i420" ; fi
if test "$videocodec_vp8" = "yes" ; then WRT_LIB_VP8="-lwebrtc_codecs_vp8" ; fi

AC_SUBST([WRT_LIB_I420])
AC_SUBST([WRT_LIB_VP8])

##
## Audio and Video IO
##

if test "$linux" = "yes" ; then
AC_ARG_WITH([alsa],
	    AC_HELP_STRING([--with-alsa],[enable Linux ALSA support.]),
	    [with_alsa="$withval"],
	    [with_alsa="yes"]
	    )
AC_ARG_WITH([pulseaudio],
	    AC_HELP_STRING([--with-pulseaudio],[enable Linux PulseAudio support.]),
	    [with_pulse="$withval"],
	    [with_pulse="no"]
	    )

if test "$with_alsa" = "yes" ; then
AC_CHECK_HEADER([alsa/asoundlib.h],,[AC_MSG_ERROR([<alsa/asoundlib.h> header not found])])
AC_CHECK_LIB(
	     [asound],
	     [snd_pcm_open],
	     [
	      LIBALSA_CFLAGS=`pkg-config alsa --cflags`
	      LIBALSA_LIBS=`pkg-config alsa --libs`
	      AC_SUBST([LIBALSA_CFLAGS])
	      AC_SUBST([LIBALSA_LIBS])
	     ],
	     [AC_MSG_ERROR([ALSA library missing])]
	    )
fi

if test "$with_pulse" = "yes" ; then
AC_CHECK_HEADER([pulse/pulseaudio.h],,[AC_MSG_ERROR([<pulse/pulseaudio.h> header not found])])
AC_CHECK_LIB(
	     [pulse],
	     [pa_threaded_mainloop_new],
	     [
	      LIBPULSE_CFLAGS=`pkg-config libpulse --cflags`
	      LIBPULSE_LIBS=`pkg-config libpulse --libs`
	      AC_SUBST([LIBPULSE_CFLAGS])
	      AC_SUBST([LIBPULSE_LIBS])
	     ],
	     [AC_MSG_ERROR([PulseAudio library missing])]
	    )
fi

AC_CHECK_HEADER([X11/Xlib.h],,[AC_MSG_ERROR([<X11/Xlib.h> header not found])])
AC_CHECK_LIB(
	     [X11],
	     [XOpenDisplay],
	     [
	      LIBX11_CXXFLAGS=`pkg-config x11 --cflags`
	      LIBX11_LIBS=`pkg-config x11 --libs`
	      AC_SUBST([LIBX11_CXXFLAGS])
	      AC_SUBST([LIBX11_LIBS])
	     ],
	     [AC_MSG_ERROR([libX11 library missing])]
	    )

AC_CHECK_HEADER([X11/extensions/XShm.h],,[AC_MSG_ERROR([<X11/extensions/XShm.h> header not found])], [#include <X11/Xlib.h>])
AC_CHECK_LIB(
	     [Xext],
	     [XShmAttach],
	     [
	      LIBXEXT_CXXFLAGS=`pkg-config xext --cflags`
	      LIBXEXT_LIBS=`pkg-config xext --libs`
	      AC_SUBST([LIBXEXT_CXXFLAGS])
	      AC_SUBST([LIBXEXT_LIBS])
	     ],
	     [AC_MSG_ERROR([libX11 library missing])]
	    )

AC_CHECK_HEADER([linux/videodev2.h],,[AC_MSG_ERROR([<linux/videodev2.h> header not found])])

fi

##
## General features
##

if test "$with_test" = "yes" ; then
	AC_MSG_WARN([Test suite is enabled])
	AC_CHECK_HEADERS(
			 [gtest/gtest.h],
			 [],
			 [AC_MSG_ERROR([<gtest/gtest.h> header not found])],
			 []
			 )
	AC_PATH_PROG([GTEST_CONFIG], gtest-config, [no])
	if test "$GTEST_CONFIG" = "no" ; then
		AC_MSG_ERROR([gtest-config was not found])
	fi
	GTEST_CXXFLAGS=`$GTEST_CONFIG --cxxflags`
	GTEST_CFLAGS=`$GTEST_CONFIG --cxxflags`
	GTEST_LIBS=`$GTEST_CONFIG --libs`
	AC_SUBST([GTEST_CXXFLAGS])
	AC_SUBST([GTEST_CFLAGS])
	AC_SUBST([GTEST_LIBS])

	AC_CHECK_HEADERS(
			 [gmock/gmock.h],
			 [],
			 [AC_MSG_ERROR([<gmock/gmock.h> header not found])],
			 []
			 )
	AC_PATH_PROG([GMOCK_CONFIG], gmock-config, [no])
	if test "$GMOCK_CONFIG" = "no" ; then
		AC_MSG_ERROR([gmock-config was not found])
	fi
	GMOCK_CXXFLAGS=`$GMOCK_CONFIG --cxxflags`
	GMOCK_CFLAGS=`$GMOCK_CONFIG --cxxflags`
	GMOCK_LIBS=`$GMOCK_CONFIG --libs`
	AC_SUBST([GMOCK_CXXFLAGS])
	AC_SUBST([GMOCK_CFLAGS])
	AC_SUBST([GMOCK_LIBS])

	AC_CHECK_HEADERS(
			 [google/gflags.h],
			 [],
			 [AC_MSG_ERROR([<google/gflags.h> header not found])],
			 []
			 )
	GFLAGS_LIBS="-lgflags"
	AC_SUBST([GFLAGS_LIBS])
else
	AC_MSG_WARN([Test suite is disabled])
fi

AC_ARG_WITH([protobuf],
	    AC_HELP_STRING([--with-protobuf],[use Protocol Buffers.]),
	    [with_protobuf="$withval"],[with_protobuf="no"])
if test "$with_protobuf" = "yes" ; then
	AC_CHECK_PROG([PROTOC], [protoc], [protoc], [], [])
	PROTOBUF_CXXFLAGS=`pkg-config protobuf --cflags`
	PROTOBUF_LIBS=`pkg-config protobuf --libs`
	AC_SUBST([PROTOBUF_CXXFLAGS])
	AC_SUBST([PROTOBUF_LIBS])
fi

##
## Output
##

COMMON_CFLAGS="-DNDEBUG -I\$(srcdir)/interface -I\$(srcdir)/main/interface -I\$(top_srcdir)/src -I\$(top_srcdir)/src/modules/interface -I./include -I./interface"
COMMON_CXXFLAGS="-DNDEBUG -I\$(srcdir)/interface -I\$(srcdir)/main/interface -I\$(top_srcdir)/src -I\$(top_srcdir)/src/modules/interface -I./include -I./interface"
AC_SUBST([COMMON_CFLAGS])
AC_SUBST([COMMON_CXXFLAGS])

AM_CONDITIONAL(WEBRTC_LINUX, test "$linux" = "yes")
AM_CONDITIONAL(WEBRTC_LINUX_ALSA, test "$with_alsa" = "yes")
AM_CONDITIONAL(WEBRTC_LINUX_PULSE, test "$with_pulse" = "yes")
AM_CONDITIONAL(WEBRTC_MAC, test "$macosx" = "yes")
AM_CONDITIONAL(WEBRTC_POSIX, test "$posix" = "yes")
AM_CONDITIONAL(WEBRTC_WINDOWS, test "$windows" = "yes")

AM_CONDITIONAL(WEBRTC_LOGGING, test "$logging" = "yes")

AM_CONDITIONAL(WITH_TEST, test "$with_test" = "yes")

AM_CONDITIONAL(WITH_SSE2, test "$has_sse2" = "yes")
AM_CONDITIONAL(WITH_NEON, test "$has_neon" = "yes")

# Audiocodecs
AM_CONDITIONAL(WEBRTC_CODEC_AMR, test "$audiocodec_amr" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_AMRWB, test "$audiocodec_amrwb" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_AVT, test "$audiocodec_avt" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_CELT, test "$audiocodec_celt" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_G722, test "$audiocodec_g722" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_G722_1, test "$audiocodec_g7221" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_G722_1C, test "$audiocodec_g7221c" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_G729, test "$audiocodec_g729" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_G729_1, test "$audiocodec_g7291" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_GSMFR, test "$audiocodec_gsmfr" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_ILBC, test "$audiocodec_ilbc" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_ISAC, test "$audiocodec_isac" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_ISACFX, test "$audiocodec_isacfx" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_OPUS, test "$audiocodec_opus" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_PCM16B, test "$audiocodec_pcm16b" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_RED, test "$audiocodec_red" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_SPEEX, test "$audiocodec_speex" = "yes")

# Videocodecs
AM_CONDITIONAL(WEBRTC_CODEC_I420, test "$videocodec_i420" = "yes")
AM_CONDITIONAL(WEBRTC_CODEC_VP8, test "$videocodec_vp8" = "yes")

AM_CONDITIONAL(WEBRTC_PROTOBUF, test "$with_protobuf" = "yes")

AC_CONFIG_FILES([
webrtc.pc
Makefile
src/Makefile
src/common_audio/Makefile
src/common_audio/resampler/Makefile
src/common_audio/signal_processing/Makefile
src/common_audio/vad/Makefile
src/common_video/Makefile
src/common_video/jpeg/Makefile
src/common_video/libyuv/Makefile
src/modules/Makefile
src/modules/audio_coding/Makefile
src/modules/audio_coding/codecs/Makefile
src/modules/audio_coding/codecs/cng/Makefile
src/modules/audio_coding/codecs/g711/Makefile
src/modules/audio_coding/codecs/g722/Makefile
src/modules/audio_coding/codecs/ilbc/Makefile
src/modules/audio_coding/codecs/iSAC/Makefile
src/modules/audio_coding/codecs/iSAC/fix/Makefile
src/modules/audio_coding/codecs/iSAC/main/Makefile
src/modules/audio_coding/codecs/pcm16b/Makefile
src/modules/audio_coding/main/Makefile
src/modules/audio_coding/neteq/Makefile
src/modules/audio_conference_mixer/Makefile
src/modules/audio_device/Makefile
src/modules/audio_device/main/Makefile
src/modules/audio_processing/Makefile
src/modules/audio_processing/utility/Makefile
src/modules/audio_processing/ns/Makefile
src/modules/audio_processing/aec/Makefile
src/modules/audio_processing/aecm/Makefile
src/modules/audio_processing/agc/Makefile
src/modules/media_file/Makefile
src/modules/rtp_rtcp/Makefile
src/modules/udp_transport/Makefile
src/modules/utility/Makefile
src/modules/video_capture/Makefile
src/modules/video_capture/main/Makefile
src/modules/video_coding/Makefile
src/modules/video_coding/codecs/Makefile
src/modules/video_coding/codecs/i420/Makefile
src/modules/video_coding/codecs/i420/main/Makefile
src/modules/video_coding/codecs/test/Makefile
src/modules/video_coding/codecs/test_framework/Makefile
src/modules/video_coding/codecs/tools/Makefile
src/modules/video_coding/codecs/vp8/Makefile
src/modules/video_coding/codecs/vp8/main/Makefile
src/modules/video_coding/main/Makefile
src/modules/video_processing/Makefile
src/modules/video_processing/main/Makefile
src/modules/video_render/Makefile
src/modules/video_render/main/Makefile
src/system_wrappers/Makefile
src/video_engine/Makefile
src/voice_engine/Makefile
src/voice_engine/main/Makefile
test/Makefile
])

AC_OUTPUT

AC_MSG_RESULT([
------------------------------------------------------------------------
  $PACKAGE $VERSION configuration.

    Compiler support:

      Target CPU: ................... ${target_cpu}
             Has NEON? .............. ${has_neon}
             Has SSE2? .............. ${has_sse2}
      Target OS: .................... ${target_os}
             Is POSIX? .............. ${posix}

    Audio configuration:

      AMR codec: ..................... ${audiocodec_amr}
      AMR-WB codec: .................. ${audiocodec_amrwb}
      AVT codec: ..................... ${audiocodec_avt}
      CELT codec: .................... ${audiocodec_celt}
      G.722 codec: ................... ${audiocodec_g722}
      G,722.1 codec: ................. ${audiocodec_g7221}
      G.722.1C codec: ................ ${audiocodec_g7221c}
      G.729 codec: ................... ${audiocodec_g729}
      G.729.1 codec: ................. ${audiocodec_g7291}
      GSM-FR codec: .................. ${audiocodec_gsmfr}
      iLBC codec: .................... ${audiocodec_ilbc}
      ISAC codec: .................... ${audiocodec_isac}
        Fixed point? ................. ${audiocodec_isacfx}
      OPUS codec: .................... ${audiocodec_opus}
      PCM16B codec: .................. ${audiocodec_pcm16b}
      RED codec: ..................... ${audiocodec_red}
      SPEEX codec: ................... ${audiocodec_speex}

      Audio IO:

        ALSA: ........................ ${with_alsa}
        PulseAudio: .................. ${with_pulse}

    Video configuration:

      I420 codec: .................... ${videocodec_i420}
      VP8 codec: ..................... ${videocodec_vp8}
        Version of libvpx library: ... ${LIBVPX_VERSION}

    General configuration:

      Enable test suite: ............. ${with_test}
      Enable logging: ................ ${logging}
      Protocol Buffers compiler ...... ${with_protobuf}

------------------------------------------------------------------------
])
