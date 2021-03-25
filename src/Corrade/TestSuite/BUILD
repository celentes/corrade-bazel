#
#   This file is part of Corrade.
#
#   Copyright © 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016,
#               2017, 2018, 2019, 2020, 2021
#             Vladimír Vondruš <mosra@centrum.cz>
#
#   Permission is hereby granted, free of charge, to any person obtaining a
#   copy of this software and associated documentation files (the "Software"),
#   to deal in the Software without restriction, including without limitation
#   the rights to use, copy, modify, merge, publish, distribute, sublicense,
#   and/or sell copies of the Software, and to permit persons to whom the
#   Software is furnished to do so, subject to the following conditions:
#
#   The above copyright notice and this permission notice shall be included
#   in all copies or substantial portions of the Software.
#
#   THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#   IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#   FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL
#   THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#   LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
#   FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER
#   DEALINGS IN THE SOFTWARE.
#
package(default_visibility = ["//visibility:public"])

CURRENT_DIR = "@corrade_src//:src/Corrade/TestSuite/"

cc_library(
    name = "TestSuite",
    srcs = [
        CURRENT_DIR + "Comparator.cpp",
        CURRENT_DIR + "Tester.cpp",
        CURRENT_DIR + "Compare/File.cpp",
        CURRENT_DIR + "Compare/FileToString.cpp",
        CURRENT_DIR + "Compare/FloatingPoint.cpp",
        CURRENT_DIR + "Compare/StringToFile.cpp",
        CURRENT_DIR + "Implementation/BenchmarkCounters.h",
        CURRENT_DIR + "Implementation/BenchmarkStats.h",
    ],
    hdrs = [
        CURRENT_DIR + "Comparator.h",
        CURRENT_DIR + "Tester.h",
        CURRENT_DIR + "TestSuite.h",
        CURRENT_DIR + "visibility.h",
        CURRENT_DIR + "Compare/FloatingPoint.h",
        CURRENT_DIR + "Compare/Container.h",
        CURRENT_DIR + "Compare/File.h",
        CURRENT_DIR + "Compare/FileToString.h",
        CURRENT_DIR + "Compare/Numeric.h",
        CURRENT_DIR + "Compare/SortedContainer.h",
        CURRENT_DIR + "Compare/StringToFile.h",
    ],
    linkopts = select({
        "@corrade//bazel/platforms:emscripten": [
            "-s", "DISABLE_EXCEPTION_CATCHING=0",
        ],
        "//conditions:default": [],
    }),
    deps = [
        "@corrade//:Utility",
    ],
)
