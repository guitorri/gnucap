# -*- Automake -*-
#
# $Id: Makefile.am,v 26.70 2008/02/05 02:03:56 al Exp $
#
# Process this file with autoconf to produce a configure script.
#
#
#                            COPYRIGHT
#
# This file is part of "Gnucap", the Gnu Circuit Analysis Package
#
#  Copyright (C) 2005 Dan McMahill
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
#  Foundation, Inc., 675 Mass Ave, Cambridge, MA 02139, USA.

bin_PROGRAMS= gnucap-modelgen
#------------------------------------------------------------------------
RAW_SRCS = \
mg_out.h mg_.h \
mg_main.cc mg_error.cc mg_in.cc mg_out_h.cc mg_out_dump.cc \
mg_out_common.cc mg_out_dev.cc mg_out_lib.cc mg_out_model.cc mg_out_root.cc
#------------------------------------------------------------------------

gnucap_modelgen_SOURCES = $(RAW_SRCS)
gnucap_modelgen_LDADD = ../lib/libgnucap.la
gnucap_modelgen_CPPFLAGS = $(AM_CPPFLAGS) -I$(top_srcdir)/include -I$(top_builddir)/include


EXTRA_DIST= \
 Make1 Make.depend Make2.g++ Make2.Debug Make2.mingw32
