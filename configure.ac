AC_PREREQ( 2.59 )

AC_INIT(
 [libodbcoci],
 [20181010],
 [jonah.harris@gmail.com])

AC_CONFIG_SRCDIR(
 [include/libodbcoci.h.in])

AM_INIT_AUTOMAKE([gnu 1.6 tar-ustar])

AC_CONFIG_MACRO_DIR([m4])

dnl Check for host type
AC_CANONICAL_HOST

dnl Check for libtool DLL support
AC_LIBTOOL_WIN32_DLL

dnl Checks for programs
AC_PROG_CC
AC_PROG_GCC_TRADITIONAL
AC_PROG_MAKE_SET
AC_PROG_INSTALL

dnl Check for libtool
AC_PROG_LIBTOOL
AC_SUBST(LIBTOOL_DEPS)

dnl Check for pkg-config
AC_PATH_PROG(PKGCONFIG,[pkg-config])

dnl Support of internationalization (i18n)
AM_GNU_GETTEXT([external])
AM_GNU_GETTEXT_VERSION([0.18.1])

dnl Check for compiler language support
AC_C_CONST
AC_C_VOLATILE

dnl Check for large file support
AC_SYS_LARGEFILE

dnl Check if WINAPI support should be enabled
AX_COMMON_CHECK_ENABLE_WINAPI

dnl Check if verbose output should be enabled
AX_COMMON_CHECK_ENABLE_VERBOSE_OUTPUT

dnl Check if debug output should be enabled
AX_COMMON_CHECK_ENABLE_DEBUG_OUTPUT

dnl Check for type definitions
AX_TYPES_CHECK_LOCAL

dnl Check if common required headers and functions are available
AX_PTHREAD_CHECK_ENABLE

dnl Check if common required headers and functions are available
AX_COMMON_CHECK_LOCAL

dnl Check if libodbcoci required headers and functions are available
AX_LIBODBCMYSQL_CHECK_LOCAL

dnl Check if tests required headers and functions are available
AX_TESTS_CHECK_LOCAL

dnl Check if DLL support is needed
AS_IF(
 [test "x$enable_shared" = xyes],
 [AS_CASE(
  [$host],
  [*cygwin* | *mingw* | *msys*],
  [AC_DEFINE(
   [HAVE_DLLMAIN],
   [1],
   [Define to 1 to enable the DllMain function.])
  AC_SUBST(
   [HAVE_DLLMAIN],
   [1])

  AC_SUBST(
   [LIBODBCMYSQL_DLL_EXPORT],
   ["-DLIBODBCMYSQL_DLL_EXPORT"])

  AC_SUBST(
   [LIBODBCMYSQL_DLL_IMPORT],
   ["-DLIBODBCMYSQL_DLL_IMPORT"])
  ])
 ])

dnl Set additional compiler flags
CFLAGS="$CFLAGS -Wall";

dnl Check if requires and build requires should be set in spec file
AS_IF(
 [test "x$ac_cv_libcerror" = xyes || test "x$ac_cv_libcthreads" = xyes || test "x$ac_cv_libcdata" = xyes || test "x$ac_cv_libcnotify" = xyes || test "x$ac_cv_libfcache" = xyes],
 [AC_SUBST(
  [libodbcoci_spec_requires],
  [Requires:])
 ])

dnl Set the date for the dpkg files
AC_SUBST(
 [DPKG_DATE],
 [`date -R 2> /dev/null`])

dnl Set the date for the spec file
AC_SUBST(
 [SPEC_DATE],
 [`date +"%a %b %e %Y" 2> /dev/null`])

dnl Generate Makefiles
AC_CONFIG_FILES([Makefile])
AC_CONFIG_FILES([include/Makefile])
AC_CONFIG_FILES([common/Makefile])
AC_CONFIG_FILES([libodbcoci/Makefile])
AC_CONFIG_FILES([po/Makefile.in])
AC_CONFIG_FILES([po/Makevars])
AC_CONFIG_FILES([msvscpp/Makefile])
dnl Generate header files
AC_CONFIG_FILES([include/libodbcoci.h])
dnl Generate distribution specific files
AC_CONFIG_FILES([dpkg/changelog])
AC_CONFIG_FILES([libodbcoci/libodbcoci.rc])
AC_CONFIG_FILES([libodbcoci.pc])
AC_CONFIG_FILES([libodbcoci.spec])
dnl Generate a source configuration file
AC_CONFIG_HEADERS([common/config.h])

AC_OUTPUT

dnl Print a summary
#AC_MSG_NOTICE([
#Building:
#   libcerror support:       $ac_cv_libcerror
#   libcthreads support:     $ac_cv_libcthreads
#   libcdata support:        $ac_cv_libcdata
#   libcnotify support:      $ac_cv_libcnotify
#   libfcache support:       $ac_cv_libfcache
#
#Features:
#   Multi-threading support: $ac_cv_libcthreads_multi_threading
#   Verbose output:          $ac_cv_enable_verbose_output
#   Debug output:            $ac_cv_enable_debug_output
#]);

