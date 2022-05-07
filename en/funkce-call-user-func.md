PHP function call_user_func()
=============================

> id: '994791e4-966a-4f32-b72d-c236177cbe0d'
> slug:
> 	cs: funkce-call-user-func
> 	en: php-function-call-user-func
> 
> publicationDate: '2019-09-11 10:04:03'
> mainCategoryId: '0eeab3a7-a54b-46db-a253-ca6100145648'
> sourceContentHash: d2414e4704bf03408ee9cc6307742bf8

Availability in `PHP 4.0`

Call a user function given by the first parameter


Parameters
--------------

| Parameter | Data type | Default value | Note |
|-----|-----|-----|-----|
| `$function` | `callback` | *not* | The function to be called. Class methods may also be invoked statically using this function by passing array($classname, $methodname) to this parameter. Additionally class methods of an object instance may be called by passing array($objectinstance, $methodname) to this parameter. |
| `$parameter` | `mixed` | null, | Zero or more parameters to be passed to the function. |
| `$_` | `mixed` | null | |


Return values
----------------

`mixed`

the function result, or false on error.

Other resources
------------

[Official documentation for call-user-func](https://www.php.net/manual/en/function.call-user-func.php)