---
title: Unit Tests, Code Coverage, and Static Analysis for C++
classes: wide
tag: Testing
---
This tutorial will cover basic usage of several testing tools for C++ code. This includes
[Google Test](https://google.github.io/googletest/) for unit testing, XXX for code coverage analysis, and XXX for static
analysis. It will show you how to incorporate them into a project, including running them with GitHub Actions.

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

This code can be found under the *testless* tag in the `src/classify_triangle.cpp` file. In addition, this repository
also contains files for VS Code, Docker, and CMake. CMake is required for this guide, but the others are not. There is
also a simple example implementation that just calls the function with some arbitrary arguments.

# Part One: Unit Tests #
This next part will demonstrate how to add unit tests with [Google Test](https://google.github.io/googletest/). There
are several different unit testing frameworks out there, but this is a fairly popular one with good documentation. In
fact, almost everything covered here can also be found in their documentation in one way or another. Additionally, they
cover several advance usages that are not covered here. This tutorial includes just the basics on getting it integrated.

## CMakeLists.txt ##

The first step is to include the Google Test code in your project. If you are using CMake v3.11 or newer, this is simply
done using CMake's FetchContent and CTest modules.

```cmake
set(CMAKE_CXX_STANDARD 11)
include(CTest)
# Only do all the testing if requested (i.e. BUILD_TESTING=ON). Default is ON.
if(BUILD_TESTING)
  # Use FetchContent to retrieve the Google Test source code.
  include(FetchContent)
  FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG main
  )
  FetchContent_MakeAvailable(googletest)
  # After Google Test is available, it still needs included in the project.
  include(GoogleTest)
  # Create the testing executable.
  add_executable(test_classifyTriangle
    test/test_classifyTriangle.cpp
  )
  target_link_libraries(test_classifyTriangle
    gtest_main
    triangle_classifier
  )
  # Tell CTest about the testing code. This is preferable to add_test as it
  # provides more information at test time to CTest.
  gtest_discover_tests(test_classifyTriangle)
endif(BUILD_TESTING)
```

Let's walk through each part and discuss what it does.

```cmake
set(CMAKE_CXX_STANDARD 11)
```

First, Google Test requires C++11 or greater, so this sets the correct required version.

```cmake
include(CTest)
# Only do all the testing if requested (i.e. BUILD_TESTING=ON). Default is ON.
if(BUILD_TESTING)
  # Other code here
endif(BUILD_TESTING)
```

Then, include the CTest module into your project. The if statement allows you to skip building the tests if desired.
This is useful when compiling for production or other cases where the tests may no longer be necessary.

```cmake
# Use FetchContent to retrieve the Google Test source code.
  include(FetchContent)
  FetchContent_Declare(
    googletest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG main
  )
  FetchContent_MakeAvailable(googletest)
  # After Google Test is available, it still needs included in the project.
  include(GoogleTest)
```

The next part instructs CMake to download Google Test during configuration. Specifically the four commands:

1. Tells CMake to load FetchContent
2. Uses FetchContent to identify a module to include, including the specific Git tag/branch to checkout
3. Instructs CMake to go ahead and download/make that module
4. Include the module in your project

The FetchContent module can fetch from Git repositories, SVN repositories, and URL locations of other CMake-based
projects. By specifying modules this way, you avoid the need to retrieve the content manually or using Git Submodules.
This also keeps your repository cleaner. However, it runs at configure time, so each time you touch your CMakeLists.txt
file, it will download again. For Google Test, this isn't too slow, but the configure time can add up if you are
fetching many different modules.

For a good explanation of FetchContent, see
[this blog post](https://ibob.bg/blog/2020/01/13/cmake-package-management/?utm_source=pocket_mylist)

```cmake
add_executable(test_classifyTriangle
  test/test_classifyTriangle.cpp
)
target_link_libraries(test_classifyTriangle
  gtest_main
  triangle_classifier
)
# Tell CTest about the testing code. This is preferable to add_test as it
# provides more information at test time to CTest.
gtest_discover_tests(test_classifyTriangle)
```

This last part is your usual executable definition. The only things to note are that you still need to define an
executable for your tests. It can be one or many, depending on how many you need and your organization strategy. You
also need to link against the gtest_main library so it gets included when compiling. Lastly, you pass the name of the
executable to CTest with a special command instead of the usual. According to
[the documentation](https://cmake.org/cmake/help/git-stage/module/GoogleTest.html), this is more robust than plain
`add_test`.

Note that since this library has only one function, I am defining a single test executable to test it. This also
explains the mixed case, since it is testing a function called *classifyTriangle*, not *classify_triangle*. Ultimately,
the names don't matter as long as you are consistent with your name scheme.

## Test File ##

After finishing this CMake, we then create the *test/test_classifyTriangle.cpp* file that will actually run the tests.
A snippet of it is shown below.

```cpp
#include <gtest/gtest.h>

#include "classify_triangle.h"

/// @test Test that equilateral triangles are correctly identified.
TEST(classifyTriangle, test_equilateral) {
  classify_triangle::TriangleType result =
      classify_triangle::classifyTriangle(1.0, 1.0, 1.0);
  ASSERT_EQ(result, classify_triangle::TriangleType::EQUILATERAL);
}
```

You need to include the gtest code, which is all done with a single include statement. You also need to include the
definitions of whatever it is you are testing. After that, you write out each test. The one shown here is on the simpler
side. The first argument for TEST is the name of the test suite while the second is the name of this specific test.
These will be shown on the result page, so provide good names.

Then, the function should perform whatever operations it needs to test and comparisons. In this case, it is testing for
equality between the result and the expected category. `ASSERT_*` tests will stop the particular test if they fail,
while `EXPECT_*` will only note the failure and try the rest of the function.

Notably, if you linked to *gtest_main* you do not need to include any *main* function in your test code. Google Test
will automatically create one. Additionally, this example only scratches the surface of different ways to write tests.
Their site has a bunch of details, including creating classes and conducting build up and tear down operations.

From here, write out all of the tests that you want. There are a ton of different paradigms for what gets tested. In
this particular example, I tried to write one per specific special case. So there is one test for equilateral triangles,
one for isosceles (including verifying that the non-equal side can be in any argument), one for scalene. There is also
one to verify that arguments are greater than zero. Lastly, there is another test to verify that
[the triangle inequality](https://en.wikipedia.org/wiki/Triangle_inequality) holds for the arguments. Without this, the
numbers the user provides may not indicate an actual, geometrically possible triangle!

After writing your tests, you should be able to configure and compile everything without issue. Then, you run the tests
with the following command from within wherever the code was built.
```bash
ctest
```
This will run every test referenced in the *gtest_discover_tests* functions in your CMakeLists.txt file. It will run
them and provide the results to the terminal. The *-VV* argument provides extra information even for passed tests. You
will get an output like so:

```bash
Test project /workspaces/cpp-unit-test-example/build
    Start 1: classifyTriangle.test_equilateral
1/5 Test #1: classifyTriangle.test_equilateral ...........   Passed    0.07 sec
    Start 2: classifyTriangle.test_isosceles_order
2/5 Test #2: classifyTriangle.test_isosceles_order .......***Failed    0.08 sec
    Start 3: classifyTriangle.test_scalene
3/5 Test #3: classifyTriangle.test_scalene ...............   Passed    0.06 sec
    Start 4: classifyTriangle.test_nonpositive_numbers
4/5 Test #4: classifyTriangle.test_nonpositive_numbers ...***Failed    0.06 sec
    Start 5: classifyTriangle.test_triangle_inequality
5/5 Test #5: classifyTriangle.test_triangle_inequality ...***Failed    0.06 sec

40% tests passed, 3 tests failed out of 5

Total Test time (real) =   0.51 sec

The following tests FAILED:
          2 - classifyTriangle.test_isosceles_order (Failed)
          4 - classifyTriangle.test_nonpositive_numbers (Failed)
          5 - classifyTriangle.test_triangle_inequality (Failed)
Errors while running CTest
```

As shown, several of our tests don't pass. This is actually good! Assuming the tests don't have bugs, you can now focus
on changing the code as needed to pass all the tests. Using this method, I have found that I tend to finish my code a
lot quicker, even if writing the tests takes a while. The tricky part is ensuring that the tests sufficiently cover
every case (more on that next time).

In this case, the tests helped identify a few issues. First, I had to ensure the order of the sides didn't matter in the
logic. (e.g. so (3, 3, 5) and (3, 5, 3) are both isosceles triangles). I also had to add logic to ensure that the
arguments provided could actually form a triangle. This involved deciding to throw exceptions if they could not, which
was not featured in the original code. There are other ways these errors could be handled though.

After making all those changes, my tests fully pass.

```bash
Test project /workspaces/cpp-unit-test-example/build
    Start 1: classifyTriangle.test_equilateral
1/5 Test #1: classifyTriangle.test_equilateral ...........   Passed    0.04 sec
    Start 2: classifyTriangle.test_isosceles_order
2/5 Test #2: classifyTriangle.test_isosceles_order .......   Passed    0.04 sec
    Start 3: classifyTriangle.test_scalene
3/5 Test #3: classifyTriangle.test_scalene ...............   Passed    0.04 sec
    Start 4: classifyTriangle.test_nonpositive_numbers
4/5 Test #4: classifyTriangle.test_nonpositive_numbers ...   Passed    0.05 sec
    Start 5: classifyTriangle.test_triangle_inequality
5/5 Test #5: classifyTriangle.test_triangle_inequality ...   Passed    0.05 sec

100% tests passed, 0 tests failed out of 5

Total Test time (real) =   0.33 sec
```

So by using Google Test for unit tests, I helped improve my code quality. It is easy to integrate in CMake, to make it
very simple to include in any project that is already using CMake. After defining a number of useful tests, the output
can then guide my development.

The upgraded code with unit tests is found in [this repository](https://github.com/kylerobots/cpp-unit-test-example),
under the *unit-test* tag.