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
load("@emsdk//emscripten_toolchain:wasm_rules.bzl", "wasm_cc_binary")
load("@build_bazel_rules_nodejs//:index.bzl", "nodejs_test")

CURRENT_DIR = "@corrade_src//:src/Corrade/Containers/Test/"

[cc_test(
    name = "Containers%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/Containers:headers",
    ],
    copts = ["-std=c++20"],
) for t in [
    "ArrayStlSpanTest",
    "ArrayViewStlSpanTest",
    "EnumSetTest",
    "GrowableArraySanitizerFailTest",
    "OptionalStlTest",
    "PointerStlTest",
    "RawForwardListTest",
    "ReferenceStlTest",
    "ReferenceTest",
    "ScopeGuardTest",
    "SequenceHelpersTest",
    "StaticArrayStlSpanTest",
    "StaticArrayTest",
    "StaticArrayViewStlSpanTest",
    "StaticArrayViewStlTest",
    "StringStlTest",
    "StringViewStlTest",
    "TagsTest",
]]

[cc_test(
    name = "Containers%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/Containers:headers",
    ],
    local_defines = ["CORRADE_GRACEFUL_ASSERT"]
) for t in [
    "LinkedListTest",
    "ArrayTest",
    "ArrayViewStlTest",
    "ArrayViewTest",
    "OptionalTest",
    "GrowableArrayTest",
    "BigEnumSetTest",
    "PointerTest",
    "StaticArrayViewTest",
    "StridedArrayViewTest",
]]

[cc_test(
    name = "Containers%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/Containers:headers",
        "//src/Corrade/Utility:UtilityTestLib",
    ],
    local_defines = ["CORRADE_GRACEFUL_ASSERT"]
) for t in [
    "StringTest",
    "StringViewTest",
]]

[cc_test(
    name = "Containers%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/Containers:headers",
        "//src/Corrade/Utility:UtilityTestLib",
    ],
) for t in [
    "ArrayTupleTest",
]]

[[wasm_cc_binary(
    name = "%s_wasm" % t,
    cc_target = ":Containers%s" % t,
    testonly = True,
  ),
  nodejs_test(
    name = "Emscripten_%s" % t,
    data = [":%s_wasm" % t],
    entry_point = ":%s_wasm/Containers%s.js" % (t, t),
  )]
for t in [
    "ArrayStlSpanTest",
    "ArrayViewStlSpanTest",
    "EnumSetTest",
    "OptionalStlTest",
    "PointerStlTest",
    "RawForwardListTest",
    "ReferenceStlTest",
    "ScopeGuardTest",
    "SequenceHelpersTest",
    "StaticArrayTest",
    "StringStlTest",
    "StringViewStlTest",
    "TagsTest",
    "LinkedListTest",
    "ArrayTest",
    "ArrayViewStlTest",
    "ArrayViewTest",
    "OptionalTest",
    "GrowableArrayTest",
    "BigEnumSetTest",
    "PointerTest",
    "StaticArrayViewTest",
    "StridedArrayViewTest",
    "StringTest",
    "StringViewTest",
    "ArrayTupleTest",
    "GrowableArraySanitizerFailTest",
    "ReferenceTest",
    "StaticArrayStlSpanTest",
    "StaticArrayViewStlSpanTest",
    "StaticArrayViewStlTest",
]]
