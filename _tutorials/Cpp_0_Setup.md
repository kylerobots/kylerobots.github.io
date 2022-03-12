---
title: "C++ Testing Part 0: Setup"
classes: wide
tag: Testing
---
This is part of a series covering basic usage of several testing tools for C++ code. This includes
[Google Test](https://google.github.io/googletest/) for unit testing, [gcovr](https://gcovr.com/en/stable/index.html)
for test coverage metrics, and [Clang-Tidy](https://clang.llvm.org/extra/clang-tidy/) for static analysis. This series
will show you how to incorporate each tool into a project.

This is Part 0 of the series that sets up the code base without any testing functionality.

# Why Test? #
There are a ton of blogs out there extolling the virtues of testing. I won't rehash that all here. Simply, testing goes
a long way to improving code quality. Even if you only implement a little bit, testing can help you find bugs early on
and help prevent bugs later when you add new features. It is worth your time to perform testing.

# Getting Started: Triangle Classification #
It's best to learn by example, so this guide will use a simple C++ library as it's test candidate. This library can be
[found on GitHub](https://github.com/kylerobots/cpp-unit-test-example). We start with no test tools and slowly add them
in each section of the guide. The library in question will help us perform triangle classification! If you remember from
school, triangles fall into one of three categories depending on the relative length of their three sides (ignoring
right triangles). The categories are:

| Category | Description |
| --- | --- |
| Equilateral | All three sides are the same length |
| Isosceles | Two sides are the same length and the other is different |
| Scalene | All three sides are different lengths |

This library provides a function that takes the three side lengths as arguments and returns the category type,
represented as an enum. The initial code for this function is shown below. If you inspect the code closely, you might be
able to spot some errors. However, the goal is to identify these faults with our different test tools.

```cpp
TriangleType classify_triangle(double side1, double side2, double side3) {
  if (side1 == side2 && side2 == side3) {
    return TriangleType::EQUILATERAL;
  } else if (side1 == side2 && side2 != side3) {
    return TriangleType::ISOSCELES;
  } else {
    return TriangleType::SCALENE;
  }
}
```

This code is found in [this repository](https://github.com/kylerobots/cpp-unit-test-example), under the *testless* tag.
In addition, this repository also contains files for VS Code, Docker, and CMake. CMake is required for this guide, but
the others are not. There is also a simple example implementation that just calls the function with some arbitrary
arguments.