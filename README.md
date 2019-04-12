# Fast vector

A faster analogue of the std::vector for the perfomance-dependent enviroment

## Features

* No default zero initialization
* Optimizations for the trivial types
* Modifiable growth factor
* No exceptions, assertions only

## Design reasoning

Most of the time zero initialization is useless, based on that it was removed from the implementation.
It is safe to reallocate memory which contains trivial data. Trivial type constructors and destructors do nothing, so there are no reasons to call them.
A growth factor of two is not always suitable for a concrete task, so it was left modifiable.
Exceptions are slow and are not used in the perfomance critical enviroment. Assertions, on the other hand, provide no overhead in release builds and are fast enough in debug builds.
