# Makefile for gperf/src

# Copyright (C) 1989, 1992, 1993, 1998, 2000, 2002, 2006 Free Software Foundation, Inc.
# Written by Douglas C. Schmidt <schmidt@ics.uci.edu>
# and Bruno Haible <bruno@clisp.org>.
#
# This file is part of GNU GPERF.
#
# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

#### Start of system configuration section. ####

# Directories used by "make":
srcdir = .

# Directories used by "make install":
prefix = /usr/local
local_prefix = /usr/local
exec_prefix = ${prefix}
bindir = ${exec_prefix}/bin

# Programs used by "make":
# C compiler
CC = gcc
CFLAGS = -g -O2
CPP = gcc -E
# C++ compiler
CXX = g++
CXXFLAGS = -g -O2
CXXCPP = g++ -E
# Both C and C++ compiler
LDFLAGS = 
OBJEXT = o
EXEEXT = .exe
# Other
MV = mv
LN = ln
RM = rm -f


# Programs used by "make install":
INSTALL = /usr/bin/install -c
INSTALL_PROGRAM = $(INSTALL)
INSTALL_DATA = $(INSTALL) -m 644
MKINSTALLDIRS = $(SHELL) $(srcdir)/../mkinstalldirs

#### End of system configuration section. ####

SHELL = /bin/sh



OBJECTS  = version.$(OBJEXT) positions.$(OBJEXT) options.$(OBJEXT) keyword.$(OBJEXT) keyword-list.$(OBJEXT) \
           input.$(OBJEXT) bool-array.$(OBJEXT) hash-table.$(OBJEXT) search.$(OBJEXT) output.$(OBJEXT) main.$(OBJEXT)
LIBS     = ../lib/libgp.a -lm
CPPFLAGS = -I. -I$(srcdir)/../lib

TARGETPROG = gperf$(EXEEXT)

all : $(TARGETPROG)

$(TARGETPROG): $(OBJECTS)
	$(CXX) $(CXXFLAGS) $(LDFLAGS) -o $@ $(OBJECTS) $(LIBS)

# Don't use implicit rules, since AIX "make" and OSF/1 "make" don't always
# expand $< correctly in this context.
#
#%.o : %.c
#	$(CC) $(CFLAGS) $(CPPFLAGS) -c $<
#
#%.o : %.cc
#	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $<

# Dependencies.
CONFIG_H = config.h
VERSION_H = version.h
POSITIONS_H = positions.h positions.icc
OPTIONS_H = options.h options.icc $(POSITIONS_H)
KEYWORD_H = keyword.h keyword.icc
KEYWORD_LIST_H = keyword-list.h keyword-list.icc $(KEYWORD_H)
INPUT_H = input.h $(KEYWORD_LIST_H)
BOOL_ARRAY_H = bool-array.h bool-array.icc $(OPTIONS_H)
HASH_TABLE_H = hash-table.h $(KEYWORD_H)
SEARCH_H = search.h $(KEYWORD_LIST_H) $(POSITIONS_H) $(BOOL_ARRAY_H)
OUTPUT_H = output.h $(KEYWORD_LIST_H) $(POSITIONS_H)

version.$(OBJEXT): version.cc $(VERSION_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/version.cc
positions.$(OBJEXT): positions.cc $(POSITIONS_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/positions.cc
options.$(OBJEXT): options.cc $(OPTIONS_H) $(VERSION_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/options.cc
keyword.$(OBJEXT): keyword.cc $(KEYWORD_H) $(POSITIONS_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/keyword.cc
keyword-list.$(OBJEXT): keyword-list.cc $(KEYWORD_LIST_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/keyword-list.cc
input.$(OBJEXT): input.cc $(INPUT_H) $(OPTIONS_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/input.cc
bool-array.$(OBJEXT): bool-array.cc $(BOOL_ARRAY_H) $(OPTIONS_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/bool-array.cc
hash-table.$(OBJEXT): hash-table.cc $(HASH_TABLE_H) $(OPTIONS_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/hash-table.cc
search.$(OBJEXT): search.cc $(SEARCH_H) $(OPTIONS_H) $(HASH_TABLE_H) $(CONFIG_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/search.cc
output.$(OBJEXT): output.cc $(OUTPUT_H) $(OPTIONS_H) $(VERSION_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/output.cc
main.$(OBJEXT): main.cc $(OPTIONS_H) $(INPUT_H) $(SEARCH_H) $(OUTPUT_H)
	$(CXX) $(CXXFLAGS) $(CPPFLAGS) -c $(srcdir)/main.cc

install : all force
	$(MKINSTALLDIRS) $(DESTDIR)$(bindir)
	$(INSTALL_PROGRAM) $(TARGETPROG) $(DESTDIR)$(bindir)/$(TARGETPROG)

installdirs : force
	$(MKINSTALLDIRS) $(DESTDIR)$(bindir)

uninstall : force
	$(RM) $(DESTDIR)$(bindir)/$(TARGETPROG)

check : all

mostlyclean : clean

clean : force
	$(RM) *~ *.s *.$(OBJEXT) *.a $(TARGETPROG) core

distclean : clean
	$(RM) config.status config.log config.cache Makefile config.h

maintainer-clean : distclean

force :
