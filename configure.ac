AC_PREREQ(2.52)

AC_INIT([Apertium Bangla-English], [0.1.0], [apertium-stuff@lists.sourceforge.net], [apertium-bn-en], [https://wiki.apertium.org/wiki/Apertium-bn-en])
AM_INIT_AUTOMAKE
AC_PROG_AWK

PKG_CHECK_MODULES(APERTIUM, apertium >= 3.6.0)
PKG_CHECK_MODULES(LTTOOLBOX, lttoolbox >= 3.5.0)

PKG_CHECK_MODULES(REGTEST, apertium-regtest >= 0.0.1, [],
                  [AC_MSG_WARN([Running tests requires apertium-regtest])])

AP_MKINCLUDE
AC_OUTPUT([Makefile])
