#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.
# $Id$
#
#                            COPYRIGHT
#
#  Copyright (C) 2005, 2006 Dan McMahill
#
#  This program is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License as published by
#  the Free Software Foundation; either version 3 of the License, or
#  (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License
#  along with this program; if not, write to the Free Software
#  Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA
#  02110-1301, USA.

AC_PREREQ(2.64)
# this is any file in the source directory
# used as a check to be sure we found it

AC_INIT([gnucap], [20160724])
AM_INIT_AUTOMAKE([-Wno-portability -Wall silent-rules])
AC_CONFIG_MACRO_DIR([m4])
AM_CONFIG_HEADER([config.h])
AM_SILENT_RULES([yes])

AM_PROG_AR
LT_INIT([disable-static])

AC_MSG_CHECKING([if debug code should be compiled in])
AC_ARG_ENABLE([debug],
[  --enable-debug            Enable building of debug code. [[default: disabled]]],
[
if test "X$enable_debug" = "Xno" ; then
	AC_MSG_RESULT([no])
else
	AC_MSG_RESULT([yes])
	enable_debug=yes
fi
],
[
	AC_MSG_RESULT([no])
	enable_debug=no
])

# Checks for programs.
AC_PROG_CXX
AC_PROG_AWK
AC_PROG_CC
AC_PROG_CPP
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_PROG_MKDIR_P
AC_CHECK_PROG(GIT,git,yes)
AC_MSG_CHECKING([for git repo])
AS_IF([test x"$GIT" = "xyes" && test -d $srcdir/.git],
      [have_git_repo=yes],
      [have_git_repo=no])
AC_MSG_RESULT([$have_git_repo])

WHICH_MAKE=`which make`
AC_SUBST([WHICH_MAKE])

AH_TEMPLATE(HAVE_GIT_REPO, "whether this is built from git")
AH_TEMPLATE(GIT_BRANCH, "the current branch")
AH_TEMPLATE(GIT_TAG, "the description")
AH_TEMPLATE(GIT_COMMIT, "the commit id")

AM_CONDITIONAL([HAVE_GIT_REPO], [test yes = $have_git_repo])
AS_IF([test yes = $have_git_repo],
      [AC_MSG_NOTICE([building from git])
       git_commit=`git rev-parse HEAD`
       git_tag=`git describe`
       git_branch=`git rev-parse --abbrev-ref HEAD`
       AC_DEFINE(HAVE_GIT_REPO)
      ])

# hmmm...
# AC_SUBST(GIT_COMMIT, $git_commit)
# AC_SUBST(GIT_BRANCH, $git_branch)
# AC_SUBST(GIT_TAG, $git_tag)

# If we are cross compiling, then we need to search for a
# gnucap-modelgen program to use for our build.  This can
# either be an installed modelgen or it can be specified
# like:
#   env MODELGEN=/build/i686--linux/modelgen/gnucap-modelgen /srcs/gnucap/configure
#           --host=alpha--netbsd --build=i686--linux
#
if test "$cross_compiling" = yes; then
	AC_PATH_PROG(MODELGEN, gnucap-modelgen)
else
	MODELGEN=../modelgen/gnucap-modelgen
	AC_SUBST([MODELGEN])
fi

# for building the documentation
#AC_PATH_PROG(DVIPDFM, dvipdfm, notfound)
#AM_CONDITIONAL(MISSING_DVIPDFM, test x$DVIPDFM = xnotfound)
#AC_PATH_PROG(HACHA, hacha, notfound)
#AC_PATH_PROG(HEVEA, hevea, notfound)
#AM_CONDITIONAL(MISSING_HEVEA, test x$HEVEA = xnotfound -o x$HACHA = xnotfound)
#AC_PATH_PROG(LATEX, latex, notfound)
#AC_PATH_PROG(MAKEINDEX, makeindex, notfound)
#AM_CONDITIONAL(MISSING_LATEX, test x$LATEX = xnotfound -o x$MAKEINDEX = xnotfound)

# Checks for libraries.

# this is a c++ program so use c++ for the tests
AC_LANG([C++])

#AC_CHECK_LIB([termcap], [main])	
#AC_CHECK_LIB([readline], [main])
AC_ARG_WITH([readline],
[AS_HELP_STRING([--with-readline],
  [support command line editing @<:@default=yes@:>@])],
[],
[with_readline=yes])

if test "x$with_readline" != xno ; then
	AC_CHECK_LIB([termcap], [main])	
	AC_CHECK_LIB([readline], [main])
fi

AC_CHECK_LIB([dl], [dlopen])

# Checks for header files.
#AC_CHECK_HEADERS([fcntl.h unistd.h])

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

if test "$enable_debug" = "yes" ; then
	CPPFLAGS="$CPPFLAGS -DTRACE_UNTESTED"
else
	CPPFLAGS="$CPPFLAGS -DNDEBUG"
fi
# if we have gcc and we've asked for debugging then add lots of -W
if test "x$GCC" = "xyes" -a "$enable_debug" = "yes"; then
	for flag in -DTRACE_UNTESTED -Wall -W -Wno-sign-compare \
		-Wpointer-arith -Wcast-qual \
		-Wwrite-strings -Wconversion \
		-Woverloaded-virtual -O2 -Wlong-long \
		-Wsign-compare -Wcast-align ; do
		case " ${CFLAGS} " in
			*\ ${flag}\ *)
				# flag is already present
				;;
			*)
				CFLAGS="$CFLAGS ${flag}"
				;;
		esac
		case " ${CXXFLAGS} " in
			*\ ${flag}\ *)
				# flag is already present
				;;
			*)
				CXXFLAGS="$CXXFLAGS ${flag}"
				;;
		esac
	done
fi

# set symbols export and loader flags according to platform
AC_CANONICAL_HOST
case $host_os in
  *linux*)
    GNUCAP_LDFLAGS="-Wl,-rpath,${pkglibdir}"
    LIBGNUCAP_LDFLAGS="$LDFLAGS -rdynamic -Wl,--enable-new-dtags -Wl,-rpath,${pkglibdir}"
    ;;
  *darwin*)
    GNUCAP_LDFLAGS="-Wl,-rpath,${pkglibdir}"
    LIBGNUCAP_LDFLAGS="$LDFLAGS -dynamiclib -Wl,-rpath,${pkglibdir}"
    ;;
esac
AC_SUBST(GNUCAP_LDFLAGS)
AC_SUBST(LIBGNUCAP_LDFLAGS)


# workaround, as we don't want to know the names literally
AC_CONFIG_SUBDIRS()
for i in `shopt -s nullglob; echo extern/*`; do
	AS_IF([test -d $i -a -x $i/configure], [subdirs="$subdirs $i"])
done

AC_CONFIG_FILES([gnucap.mk], [chmod +x gnucap.mk])
AC_CONFIG_FILES([main/gnucap-conf], [chmod +x main/gnucap-conf])
AC_CONFIG_FILES([main/gnucap], [chmod +x main/gnucap])

AC_CONFIG_FILES([
	GNUmakefile
	apps/Makefile
	include/Makefile
	lib/Makefile
	main/Makefile
	modelgen/Makefile
	tests/Makefile
	])

AC_CONFIG_COMMANDS([default])
AC_OUTPUT

plugindir=$libdir/$package

AC_MSG_RESULT([
** Configuration summary for $PACKAGE $VERSION:

   prefix:                   $prefix
   plugindir:                $plugindir
   CPPFLAGS:                 $CPPFLAGS
   CFLAGS:                   $CFLAGS
   CXXFLAGS:                 $CXXFLAGS
   LDFLAGS:                  $LDFLAGS
   LIBS:                     $LIBS
   externals:              $subdirs

])

