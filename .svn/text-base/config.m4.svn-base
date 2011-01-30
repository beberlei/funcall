dnl $Id$
dnl config.m4 for extension funcall

dnl Comments in this file start with the string 'dnl'.
dnl Remove where necessary. This file will not work
dnl without editing.

dnl If your extension references something external, use with:

dnl PHP_ARG_WITH(funcall, for funcall support,
dnl Make sure that the comment is aligned:
dnl [  --with-funcall             Include funcall support])

dnl Otherwise use enable:

PHP_ARG_ENABLE(funcall, whether to enable funcall support,
[  --enable-funcall           Enable funcall support])

if test "$PHP_FUNCALL" != "no"; then
  dnl Write more examples of tests here...

  dnl # --with-funcall -> check with-path
  dnl SEARCH_PATH="/usr/local /usr"     # you might want to change this
  dnl SEARCH_FOR="/include/funcall.h"  # you most likely want to change this
  dnl if test -r $PHP_FUNCALL/$SEARCH_FOR; then # path given as parameter
  dnl   FUNCALL_DIR=$PHP_FUNCALL
  dnl else # search default path list
  dnl   AC_MSG_CHECKING([for funcall files in default path])
  dnl   for i in $SEARCH_PATH ; do
  dnl     if test -r $i/$SEARCH_FOR; then
  dnl       FUNCALL_DIR=$i
  dnl       AC_MSG_RESULT(found in $i)
  dnl     fi
  dnl   done
  dnl fi
  dnl
  dnl if test -z "$FUNCALL_DIR"; then
  dnl   AC_MSG_RESULT([not found])
  dnl   AC_MSG_ERROR([Please reinstall the funcall distribution])
  dnl fi

  dnl # --with-funcall -> add include path
  dnl PHP_ADD_INCLUDE($FUNCALL_DIR/include)

  dnl # --with-funcall -> check for lib and symbol presence
  dnl LIBNAME=funcall # you may want to change this
  dnl LIBSYMBOL=funcall # you most likely want to change this 

  dnl PHP_CHECK_LIBRARY($LIBNAME,$LIBSYMBOL,
  dnl [
  dnl   PHP_ADD_LIBRARY_WITH_PATH($LIBNAME, $FUNCALL_DIR/lib, FUNCALL_SHARED_LIBADD)
  dnl   AC_DEFINE(HAVE_FUNCALLLIB,1,[ ])
  dnl ],[
  dnl   AC_MSG_ERROR([wrong funcall lib version or lib not found])
  dnl ],[
  dnl   -L$FUNCALL_DIR/lib -lm -ldl
  dnl ])
  dnl
  dnl PHP_SUBST(FUNCALL_SHARED_LIBADD)

  PHP_NEW_EXTENSION(funcall, funcall.c, $ext_shared)
fi
