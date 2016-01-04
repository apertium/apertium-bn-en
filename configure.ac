#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.


AC_PREREQ(2.52)

m4_define([required_apertium_version], [3.2.0])
m4_define([required_lttoolbox_version], [3.1.2])

AC_INIT([apertium-bn-en], [0.1], [lkhatiwada@users.sourceforge.net])
AM_INIT_AUTOMAKE([apertium-bn-en], [0.1], no-define)
AC_PROG_LN_S
AC_PROG_AWK

PKG_CHECK_MODULES(APERTIUM,   apertium >= required_apertium_version, [], [PKG_CHECK_MODULES(APERTIUM,   apertium-3.2 >= required_apertium_version)])
PKG_CHECK_MODULES(LTTOOLBOX, lttoolbox >= required_lttoolbox_version, [], [PKG_CHECK_MODULES(LTTOOLBOX, lttoolbox-3.2 >= required_lttoolbox_version)])


  
AC_OUTPUT([Makefile])
