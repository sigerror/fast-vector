# Fast vector

A faster analogue of the std::vector for the perfomance-dependent enviroment

## Features

* No default zero initialization
* Optimizations for the trivial types
* Modifiable growth factor
* No exceptions, assertions only

## Requirements

Make sure to use a C++17 language standart compliant compiler.

## Google benchmark results

> **Hardware:** Intel® Core™ i7-4720HQ CPU, 8GB DDR3 Dual-channel memory<br/>
> **Enviroment:** Visual Studio 2017, Windows 10 Pro 64-bit<br/>
> **Data size:** 10,000 items

### Trivial data types

```
--------------------------------------------------------------------------
Benchmark                                Time             CPU   Iterations
--------------------------------------------------------------------------
push_back | std::vector              20126 ns        19950 ns        34462
push_back | fast_vector               9392 ns         9417 ns        89600
--------------------------------------------------------------------------
reserve & push_back | std::vector    12991 ns        13114 ns        56000
reserve & push_back | fast_vector     6416 ns         6417 ns       112000
--------------------------------------------------------------------------
push_back & pop_back | std::vector   12704 ns        12835 ns        56000
push_back & pop_back | fast_vector    9253 ns         9242 ns        89600
```

### Non-trivial data types

```
--------------------------------------------------------------------------
Benchmark                                Time             CPU   Iterations
--------------------------------------------------------------------------
push_back | std::vector             137225 ns       138126 ns         3733
push_back | fast_vector             121523 ns       122768 ns         5600
--------------------------------------------------------------------------
reserve & push_back | std::vector    88303 ns        87887 ns         7467
reserve & push_back | fast_vector    88671 ns        87887 ns         7467
--------------------------------------------------------------------------
emplace_back | std::vector           87804 ns        87193 ns         8960
emplace_back | fast_vector           65897 ns        66964 ns        11200
--------------------------------------------------------------------------
push_back & pop_back | std::vector  101814 ns       100098 ns         6400
push_back & pop_back | fast_vector   96396 ns        96257 ns         7467
```

## Design reasoning

Most of the time zero initialization is useless, based on that it was removed from the implementation.<br/>
It is safe to reallocate memory which contains trivial data. Trivial type constructors and destructors do nothing, so there are no reasons to call them.<br/>
A growth factor of two is not always suitable for a concrete task, so it was left modifiable.<br/>
Exceptions are slow and are not used in the perfomance critical enviroment. Assertions, on the other hand, provide no overhead in release builds and are fast enough in debug builds.
