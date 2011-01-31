# funcall

Original repo: http://code.google.com/p/funcall/

## What?

Register pre and post processing callbacks for any function or method.

## Changelog

* Rework internal datastructure from a list to a hashtable to optimize for large callback stacks.

## TODO

* Refactor callbacks to allow any PHP callback not just strings
* Allow to modify arguments in pre callbacks.
* Reimplement fc_list() as fc_list_all()
* Implement fc_list_callbacks($function)
* Implement way to stop event propagation and function execution gracefully
* Implement ways to remove callbacks (How?)
* Add fc_add_instance_pre($instance, $method, $callback), fc_add_instance_post($instance, $method, $callback) methods to register callbacks only executed for a sepecific instance only.
* Add hook for class instantiation to allow lazy loading of callbacks for instances or classes.

