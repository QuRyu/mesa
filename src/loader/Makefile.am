# Copyright © 2012 Intel Corporation
#
# Permission is hereby granted, free of charge, to any person obtaining a
# copy of this software and associated documentation files (the "Software"),
# to deal in the Software without restriction, including without limitation
# the rights to use, copy, modify, merge, publish, distribute, sublicense,
# and/or sell copies of the Software, and to permit persons to whom the
# Software is furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice (including the next
# paragraph) shall be included in all copies or substantial portions of the
# Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL
# THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
# FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS
# IN THE SOFTWARE.

include Makefile.sources

EXTRA_DIST = SConscript

noinst_LTLIBRARIES = libloader.la

AM_CPPFLAGS = \
	$(DEFINES) \
	-I$(top_srcdir)/include \
	-I$(top_srcdir)/src \
	$(VISIBILITY_CFLAGS) \
	$(XCB_DRI3_CFLAGS) \
	$(LIBDRM_CFLAGS)

libloader_la_CPPFLAGS = $(AM_CPPFLAGS)
libloader_la_SOURCES = $(LOADER_C_FILES)
libloader_la_LIBADD =

if HAVE_DRICOMMON
libloader_la_CPPFLAGS += \
	-I$(top_builddir)/src/util/ \
	-I$(top_srcdir)/src/mesa/drivers/dri/common/ \
	-I$(top_srcdir)/src/mesa/ \
	-I$(top_srcdir)/src/mapi/ \
	-DUSE_DRICONF

libloader_la_LIBADD += \
	$(top_builddir)/src/util/libxmlconfig.la

endif

if HAVE_LIBDRM
libloader_la_LIBADD += \
	$(LIBDRM_LIBS)
endif

if HAVE_PLATFORM_X11
if HAVE_DRI3
noinst_LTLIBRARIES += libloader_dri3_helper.la

libloader_dri3_helper_la_SOURCES = \
	loader_dri3_helper.c \
	loader_dri3_helper.h
libloader_dri3_helper_la_LIBADD = $(XCB_DRI3_LIBS)
endif
endif
