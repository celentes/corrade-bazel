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

CURRENT_DIR = "@corrade_src//:src/Corrade/Test/"

corrade_configure_header(
    name = "configure",
    src = CURRENT_DIR + "configure.h.cmake",
    output = "configure.h",
    defines = {
        # TODO: this is selectable; also, why both?
        "CORRADE_TARGET_GCC": "1",
        "CORRADE_TARGET_CLANG": "1",
    },
    local = True,
)

cc_test(
    name = "MainTest",
    srcs = [CURRENT_DIR + "MainTest.cpp"],
    args = [
        "--arg-utf",
        "hýždě",
        "--arg-another",
        "šňůra",
    ],
    deps = ["@corrade//:TestSuite"],
)

cc_test(
    name = "TargetTest",
    srcs = [CURRENT_DIR + "TargetTest.cpp"],
    deps = [
        "@corrade//:TestSuite",
        ":configure",
    ],
)

cc_test(
    name = "CorradeVersionTest",
    srcs = [CURRENT_DIR + "VersionTest.cpp"],
    deps = ["@corrade//:TestSuite"],
)

cc_test(
    name = "Cpp11StandardTest",
    srcs = [CURRENT_DIR + "CppStandardTest.cpp"],
    deps = ["@corrade//:TestSuite"],
    defines = ["COMPILING_AS_CPP11"],
    copts = ["-std=c++11"],
)

cc_test(
    name = "Cpp14StandardTest",
    srcs = [CURRENT_DIR + "CppStandardTest.cpp"],
    deps = ["@corrade//:TestSuite"],
    defines = [
        "COMPILING_AS_CPP14",
        "TEST_NAME=\\\"Cpp14StandardTest\\\"",
    ],
    copts = ["-std=c++14"],
)

cc_test(
    name = "Cpp14StandardTestCMakeStandard",
    srcs = [CURRENT_DIR + "CppStandardTest.cpp"],
    deps = ["@corrade//:TestSuite"],
    defines = [
        "COMPILING_AS_CPP14",
        "CORRADE_CXX_STANDARD=17",
        "TEST_NAME=\\\"Cpp14StandardTestCMakeStandard\\\"",
    ],
    copts = ["-std=c++14"],
)

cc_test(
    name = "Cpp17StandardTestCMakeStandard",
    srcs = [CURRENT_DIR + "CppStandardTest.cpp"],
    deps = ["@corrade//:TestSuite"],
    defines = ["COMPILING_AS_CPP17"],
    copts = ["-std=c++17"],
)

cc_test(
    name = "Cpp2aStandardTestCMakeStandard",
    srcs = [CURRENT_DIR + "CppStandardTest.cpp"],
    deps = ["@corrade//:TestSuite"],
    defines = ["COMPILING_AS_CPP2A"],
    copts = ["-std=c++2a"],
)

[[wasm_cc_binary(
    name = "%s_wasm" % t,
    cc_target = ":%s" % t,
    testonly = True,
  ),
  nodejs_test(
    name = "Emscripten_%s" % t,
    data = [":%s_wasm" % t],
    entry_point = ":%s_wasm/%s.js" % (t, t),
  )]
for t in [
    "TargetTest",
    "CorradeVersionTest",
    "Cpp11StandardTest",
    "Cpp14StandardTest",
    "Cpp14StandardTestCMakeStandard",
    "Cpp17StandardTestCMakeStandard",
    "Cpp2aStandardTestCMakeStandard",
]]

[[wasm_cc_binary(
    name = "%s_wasm" % t,
    cc_target = ":%s" % t,
    testonly = True,
  ),
  nodejs_test(
    name = "Emscripten_%s" % t,
    data = [":%s_wasm" % t],
    entry_point = ":%s_wasm/%s.js" % (t, t),
    args = [
        "--arg-utf",
        "hýždě",
        "--arg-another",
        "šňůra",
    ],
  )]
for t in [
    "MainTest",
]]
