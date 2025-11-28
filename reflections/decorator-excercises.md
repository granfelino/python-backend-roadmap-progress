### Link: https://github.com/granfelino/decorator-excercises

### Reflections:
* decorators are functions which replace the original function, keeping its
    original functionality and adding some functionality on the top
* A decorator:

@decorator
def func():
    ...

unwraps to kind of this:
func = decorator(func)

* parametrized decorators are decorator factories:

@decorator(param)
def func():
    ...

decorator = decorator(param)
func = decorator(func)

* typical decorator template:

def decorator(func):
    @wraps(func)
    def wrapper(\*args, \*\*kwargs):
        return func(\*args, \*\*kwargs)
    return wrapper

def decorator(param):
    def dec(func):
        @wraps(func)
        def wrapper(\*args, \*\*kwargs):
            return func(\*args, \*\*kwargs)
        return wrapper
    return dec

* in the second example of the previous point the param is kept in the function
inside the closure -> the function's context contains param
* the @wraps decorator ensures that the metadata of the decorated function
is preserved
* the decorator factory allows for creating decorators based on the function's
signature (e.g. ex17 -> decorator works on async and sync functions)
* rate limiting, caching, timestamping, retrying, multiple calls, ensuring
parameter/return type, applying callbacks are some examples where decorators
are being very helpful
