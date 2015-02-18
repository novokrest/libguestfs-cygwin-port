# libguestfs
# Copyright (C) 2012 Red Hat Inc.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 2 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

SUBDIRS = . docs

include $(top_srcdir)/subdir-rules.mk

include $(srcdir)/Makefile.inc

generator_built = \
	$(guestfs_gobject_headers) \
	$(guestfs_gobject_sources) \
	bindtests.js

BUILT_SOURCES = $(generator_built)

EXTRA_DIST = \
	$(generator_built) \
	TODO.txt \
	.gitignore \
	bindtests-manual.js \
	docs/.gitignore \
	tests-misc.js \
	run-tests \
	run-live-tests

# Remove the old generated files which were directly in the gobject/
# directory.  These have now moved into gobject/src/
CLEANFILES = \
	guestfs-gobject*.c *.o *.lo

libname = libguestfs-gobject-1.0.la

lib_LTLIBRARIES = $(libname)

libguestfs_gobject_1_0_ladir = $(includedir)/guestfs-gobject

libguestfs_gobject_1_0_la_HEADERS = $(guestfs_gobject_headers)
libguestfs_gobject_1_0_la_SOURCES = $(guestfs_gobject_sources)
libguestfs_gobject_1_0_la_CFLAGS = -I$(top_srcdir)/src -I$(srcdir)/include \
                                   -DGUESTFS_PRIVATE=1 \
                                   $(GOBJECT_CFLAGS)
libguestfs_gobject_1_0_la_LDFLAGS = $(LDFLAGS) -L$(top_builddir)/src
libguestfs_gobject_1_0_la_LIBADD = $(top_builddir)/src/libguestfs.la $(GOBJECT_LIBS) $(GIO_LIBS)

pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libguestfs-gobject-1.0.pc

# All the headers except <guestfs-gobject.h> should be installed
# in the subdirectory.
install-data-hook:
	rm $(DESTDIR)$(includedir)/guestfs-gobject/guestfs-gobject.h
	install -m 0644 $(srcdir)/include/guestfs-gobject.h $(DESTDIR)$(includedir)

-include $(INTROSPECTION_MAKEFILE)
INTROSPECTION_GIRS =
INTROSPECTION_SCANNER_ARGS = --add-include-path=$(srcdir) --warn-all
INTROSPECTION_COMPILER_ARGS = --includedir=$(srcdir)


