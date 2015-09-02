## -*- Makefile -*-
##
## $Id: Makefile.am,v 26.136 2009/12/08 02:03:49 al Exp $
##
##                            COPYRIGHT
##
## This file is part of "Gnucap", the Gnu Circuit Analysis Package
##
##  Copyright (C) 2005, 2006 Dan McMahill
##
##  This program is free software; you can redistribute it and/or modify
##  it under the terms of the GNU General Public License as published by
##  the Free Software Foundation; either version 3 of the License, or
##  (at your option) any later version.
##
##  This program is distributed in the hope that it will be useful,
##  but WITHOUT ANY WARRANTY; without even the implied warranty of
##  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
##  GNU General Public License for more details.
##
##  You should have received a copy of the GNU General Public License
##  along with this program; if not, write to the Free Software
##  Foundation, Inc.,  51 Franklin Street, Fifth Floor, Boston, MA
##  02110-1301, USA.

lib_LTLIBRARIES = libgnucap.la
libgnucap_la_CPPFLAGS = $(AM_CPPFLAGS) -I$(top_srcdir)/include -I$(top_builddir)/include
libgnucap_la_LDFLAGS = $(AM_LDFLAGS) $(LIBGNUCAP_LDFLAGS)

libgnucap_la_SOURCES = \
globals.cc \
m_expression_dump.cc m_expression_in.cc m_expression_reduce.cc \
m_base_in.cc m_base_math.cc m_fft.cc  m_spline.cc \
ap_construct.cc ap_convert.cc ap_error.cc ap_get.cc ap_match.cc ap_skip.cc \
l_ftos.cc l_pmatch.cc l_timer.cc l_trim.cc l_wmatch.cc \
io.cc io_contr.cc io_error.cc io_findf.cc io_out.cc io_xopen.cc \
u_lang.cc u_nodemap.cc u_opt1.cc u_opt2.cc \
u_parameter.cc u_prblst.cc u_probe.cc u_sim_data.cc u_xprobe.cc \
d_subckt.cc d_logic.cc d_logicmod.cc \
e_base.cc e_card.cc e_node.cc e_model.cc e_compon.cc \
e_elemnt.cc e_ccsrc.cc e_storag.cc e_cardlist.cc \
e_paramlist.cc \
bm_cond.cc bm_value.cc bm.cc \
c__cmd.cc c_attach.cc c_file.cc \
findbr.cc plot.cc
