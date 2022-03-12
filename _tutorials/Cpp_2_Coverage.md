---
title: "C++ Testing Part 2: Test Coverage"
classes: wide
tag: Testing
---
This is part of a series covering basic usage of several testing tools for C++ code. This includes
[Google Test](https://google.github.io/googletest/) for unit testing, [gcovr](https://gcovr.com/en/stable/index.html)
for test coverage metrics, and [Clang-Tidy](https://clang.llvm.org/extra/clang-tidy/) for static analysis. This series
will show you how to incorporate each tool into a project.

This is Part 2 of the series and adds analysis of how much of the code is covered by our tests. To do this, you will use
[gcovr](https://gcovr.com/en/stable/index.html), which is a Python-based tool that uses
[gcov](https://gcc.gnu.org/onlinedocs/gcc/Gcov.html) under the hood. The documentation for the tool is fantastic and
provides a great overview of the various options it supports. The goal with this tool is to verify that as many lines of
code are executed by your unit tests as possible. This helps lend confidence that there are no hidden, untested edge
cases. However, please note that just because you have 100% coverage does not mean there are no errors.

## Installation ##
Since this tool is a Python package, you can install with pip. However, if a project is entirely C++ based, it may not
have pip on it to begin with. I found that gcovr is also in the apt store, so `apt install gcovr` is all you need to
run.

Additionally, it is important to note that this tool requires using gcc as the compiler, since gcov is a gcc tool.

## CMakeLists.txt ##
In order to collect coverage information, you have to set certain compiler flags. This can be easily done in the
CMakeLists file. While the official documentation provides
[instructions on using CMake](https://gcovr.com/en/stable/cookbook.html#out-of-source-builds-with-cmake), I actually
go about setting the compiler flags a slightly different way. Just add the following to the file before you declare any
executables or libraries that will be part of coverage analysis. Typically, this will mean this goes very close to the
beginning of the file.

``` cmake
include(CTest)
# If testing, include coverage flags when compiling.
if(BUILD_TESTING)
  add_compile_options("--coverage")
  add_link_options("--coverage")
endif(BUILD_TESTING)
```
By wrapping the flags this way, they are only added when specifically building test files. Alternatively, you could also
check for the `CMAKE_BUILD_TYPE` and use that to set the flag. The goal is to not set these flags when not testing, to
allow for better optimization and a smaller release binary.

## Analysis ##
After modifying the `CMakeLists.txt` file, you are ready to begin your analysis. Assuming you have already written your
tests, just compile and run the tests. The above flags will cause the correct data to be generated automatically.

After that, you then use gcovr to collect and report the results. Their
[user guide](https://gcovr.com/en/stable/guide.html#gcovr) has very in-depth analysis, so this guide will only hit the
highlights. From your build folder, execute the following command.

```bash
gcovr -r .. .
```

You can also add the `-b` flag to include information about branches taken. Although it is important to note that just
because every branch is tested, does not mean every condition is tested.

After some time, it will report results similar to the below output.

```
------------------------------------------------------------------------------
                           GCC Code Coverage Report
Directory: ..
------------------------------------------------------------------------------
File                                       Lines    Exec  Cover   Missing
------------------------------------------------------------------------------
build/_deps/googletest-src/googlemock/include/gmock/gmock-cardinalities.h
                                              14       0     0%   66,70-71,96,100-101,105-106,111-112,117-119,123
build/_deps/googletest-src/googlemock/include/gmock/gmock-matchers.h
                                               9       0     0%   3496-3499,3515-3516,3572-3573,3576
```

You'll notice that it lists out each file, the total number of lines within the file, the number covered by the test
program, and line numbers of any line not covered. However, this information is noisy for a few reasons. For starters,
it is including all files, including the ones associated with Google Test. Additionally, if you poke around with branch
settings, you will
[find that it sometimes flags a branch as not taken even when that isn't necessarily the case](https://gcovr.com/en/stable/faq.html#why-does-c-code-have-so-many-uncovered-branches).
To address these options, there are a few filter and exclusion flags that I run. In particular, I run the following.

```bash
gcovr -r .. --filter \.\./src/ --exclude-unreachable-branches --exclude-throw-branches .
```

The filter limits the report to only files in your src folder, as described in
[the documentation](https://gcovr.com/en/stable/guide.html#using-filters). The exclude flags address branches that the
compiler creates. The output now looks much cleaner.

```
------------------------------------------------------------------------------
                           GCC Code Coverage Report
Directory: ..
------------------------------------------------------------------------------
File                                       Lines    Exec  Cover   Missing
------------------------------------------------------------------------------
src/classify_triangle.cpp                     13      12    92%   22
src/example.cpp                               15       0     0%   5,7-20
------------------------------------------------------------------------------
TOTAL                                         28      12    42%
------------------------------------------------------------------------------
```

As you can see, it is now really simple to identify parts of the code that are not tested. Note that `example.cpp` is
not part of the test suite, so is of course reporting 0%. This is expected and additional filtering will remove it.

With this data, you can then see that the only line not covered is the else statement if no triangle type can be
determined. However, this case doesn't actually exist, because the previous clauses cover all possible situations. That
statement can be safely removed. In other projects, this can be addressed by writing additional tests to cover the
missing branches.

After changing the code and rerunning gcovr, the new table show that all lines are covered.

```
------------------------------------------------------------------------------
                           GCC Code Coverage Report
Directory: ..
------------------------------------------------------------------------------
File                                       Lines    Exec  Cover   Missing
------------------------------------------------------------------------------
src/classify_triangle.cpp                     11      11   100%   
src/example.cpp                               15       0     0%   5,7-20
------------------------------------------------------------------------------
TOTAL                                         26      11    42%
------------------------------------------------------------------------------
```

## Formatting ##
If you don't want to read through output on the command line, gcovr also offers ways to output in different formats.
The [section on outputs](https://gcovr.com/en/stable/guide.html#output-options) has a wealth of good information. For
example, you can generate HTML pages that allow you to click through each file and see which lines and branches are
covered. To do that, run the below command. It will generate several HTML files, with the primary one named whatever
you put as the `-o` argument.

```bash
gcovr -r .. --filter \.\./src/ --exclude-unreachable-branches --exclude-throw-branches --html --html-details -o report.html .
```

The resulting webpage will look something like the image below. There are a number of flags in gcovr that can tune this
format, such as by specifying the percentage of coverage required for a high, medium, or low rating.

{% include figure image_path="/assets/images/GcovOutput.png" alt="A coverage report showing 100% coverage for the file under test with a clickable filename to learn more about that particular file." caption="The main page generated by gcovr" %}

By doing this, you can easily see where your tests need to be improved, resulting in greater code quality!

The upgraded code with coverage flags and 100% coverage is found in
[this repository](https://github.com/kylerobots/cpp-unit-test-example), under the *coverage* tag.