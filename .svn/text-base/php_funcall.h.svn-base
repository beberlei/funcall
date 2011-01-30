/*
  +----------------------------------------------------------------------+
  | funcall                                                              |
  +----------------------------------------------------------------------+
  | Copyright (c) 2008 The PHP Group                                     |
  +----------------------------------------------------------------------+
  | This source file is subject to the new BSD license, that is bundled  |
  | with this package in the file LICENSE.                               |
  +----------------------------------------------------------------------+
  | Author:Surf Chen <surfchen@gmail.com>                                |
  +----------------------------------------------------------------------+
*/

/* $Id$ */

#ifndef PHP_FUNCALL_H
#define PHP_FUNCALL_H

extern zend_module_entry funcall_module_entry;
#define phpext_funcall_ptr &funcall_module_entry

#ifdef PHP_WIN32
#define PHP_FUNCALL_API __declspec(dllexport)
#else
#define PHP_FUNCALL_API
#endif

#ifdef ZTS
#include "TSRM.h"
#endif

typedef struct _fc_function_list {
    char *name;
    zval *func;
    struct _fc_callback_list *callback_ref;
    struct _fc_function_list *next;
} fc_function_list;
typedef struct _fc_callback_list {
    char *name;
    zval *func;
    struct _fc_callback_list *next;
} fc_callback_list;

PHP_MINIT_FUNCTION(funcall);
PHP_MSHUTDOWN_FUNCTION(funcall);
PHP_RINIT_FUNCTION(funcall);
PHP_RSHUTDOWN_FUNCTION(funcall);
PHP_MINFO_FUNCTION(funcall);

PHP_FUNCTION(fc_add_pre);
PHP_FUNCTION(fc_add_post);
PHP_FUNCTION(fc_list);

/* 
  	Declare any global variables you may need between the BEGIN
	and END macros here:     

*/
ZEND_BEGIN_MODULE_GLOBALS(funcall)
    fc_function_list *fc_pre_list;	
    fc_function_list *fc_post_list;	
	char *last_eval_statement;
    int use_callback;	
    zval *fc_null_zval;
ZEND_END_MODULE_GLOBALS(funcall)

#define CALLBACK_DISABLE 0
#define CALLBACK_ENABLE 1

/* In every utility function you add that needs to use variables 
   in php_funcall_globals, call TSRMLS_FETCH(); after declaring other 
   variables used by that function, or better yet, pass in TSRMLS_CC
   after the last function argument and declare your utility function
   with TSRMLS_DC after the last declared argument.  Always refer to
   the globals in your function as FUNCALL_G(variable).  You are 
   encouraged to rename these macros something shorter, see
   examples in any other php module directory.
*/

#ifdef ZTS
#define FCG(v) TSRMG(funcall_globals_id, zend_funcall_globals *, v)
#else
#define FCG(v) (funcall_globals.v)
#endif

#endif	/* PHP_FUNCALL_H */



//#define FUNCALL_DEBUG(str) fprintf(stderr,"%s",str)
#define FUNCALL_DEBUG(str) ;

#define T(offset) (*(temp_variable *)((char *) Ts + offset))
zval *fg_zval_ptr(znode *node, temp_variable *Ts TSRMLS_DC)
{
    switch (node->op_type) {
        case IS_CONST:
            return &node->u.constant;
            break;
        case IS_TMP_VAR:
            return &T(node->u.var).tmp_var;
            break;
        case IS_VAR:
            if (T(node->u.var).var.ptr) {
                return T(node->u.var).var.ptr;
            } else {
                temp_variable *T = &T(node->u.var);
                zval *str = T->str_offset.str;

                if (T->str_offset.str->type != IS_STRING
                    || ((int)T->str_offset.offset<0)
                    || (T->str_offset.str->value.str.len <= T->str_offset.offset)) {
                    zend_error(E_NOTICE, "Uninitialized string offset:  %d", T->str_offset.offset);
                    T->tmp_var.value.str.val = STR_EMPTY_ALLOC();
                    T->tmp_var.value.str.len = 0;
                } else {
                    char c = str->value.str.val[T->str_offset.offset];

                    T->tmp_var.value.str.val = estrndup(&c, 1); 
                    T->tmp_var.value.str.len = 1;
                }   
				Z_SET_REFCOUNT_P(&(T->tmp_var), 1); 
				Z_SET_ISREF_P(&(T->tmp_var));
                T->tmp_var.type = IS_STRING;
                return &T->tmp_var;
            }   
            break;
        case IS_UNUSED:
            return NULL;
            break;
    }   
    return NULL;
}

/*
 * Local variables:
 * tab-width: 4
 * c-basic-offset: 4
 * End:
 * vim600: noet sw=4 ts=4 fdm=marker
 * vim<600: noet sw=4 ts=4
 */
