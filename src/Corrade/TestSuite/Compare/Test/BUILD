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
load("@corrade//:index.bzl", "corrade_configure_header")
load("@emsdk//emscripten_toolchain:wasm_rules.bzl", "wasm_cc_binary")
load("@build_bazel_rules_nodejs//:index.bzl", "nodejs_test")

CURRENT_DIR = "@corrade_src//:src/Corrade/TestSuite/Compare/Test/"

corrade_configure_header(
    name = "configure",
    src = CURRENT_DIR + "configure.h.cmake",
    output = "configure.h",
    defines = {
        "FILETEST_DIR": "$(rootpath %sFileTestFiles)" % CURRENT_DIR,
        "FILETEST_SAVE_DIR": "$(rootpath %sFileTestFiles)/write" % CURRENT_DIR,
    },
    deps = [CURRENT_DIR + "FileTestFiles"],
    local = True,
)

[cc_test(
    name = "TestSuiteCompare%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = [
        "@corrade//:TestSuite",
        ":configure",
    ],
    data = [
        CURRENT_DIR + "FileTestFiles/base.txt",
        CURRENT_DIR + "FileTestFiles/different.txt",
        CURRENT_DIR + "FileTestFiles/empty.txt",
        CURRENT_DIR + "FileTestFiles/hýždě.txt",
        CURRENT_DIR + "FileTestFiles/smaller.txt",
    ],
)
for t in [
    "FileTest",
    "FileToStringTest",
    "StringToFileTest",
]]

[cc_test(
    name = "TestSuiteCompare%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = ["@corrade//:TestSuite"],
)
for t in [
    "ContainerTest",
    "SortedContainerTest",
    "FloatingPointTest",
    "NumericTest",
]]

[[wasm_cc_binary(
    name = "%s_wasm" % t,
    cc_target = ":TestSuiteCompare%s" % t,
    testonly = True,
  ),
  nodejs_test(
    name = "Emscripten_%s" % t,
    data = [":%s_wasm" % t],
    entry_point = ":%s_wasm/TestSuiteCompare%s.js" % (t, t),
  )]
for t in [
    "ContainerTest",
    "SortedContainerTest",
    "FloatingPointTest",
    "NumericTest",
    #"FileTest",
    #"FileToStringTest",
    #"StringToFileTest",
]]
