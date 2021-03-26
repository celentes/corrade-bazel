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
load("@corrade//:index.bzl", "corrade_configure_header", "corrade_resource")
load("@emsdk//emscripten_toolchain:wasm_rules.bzl", "wasm_cc_binary")
load("@build_bazel_rules_nodejs//:index.bzl", "nodejs_test")

CURRENT_DIR = "@corrade_src//:src/Corrade/Utility/Test/"

corrade_configure_header(
    name = "configure",
    src = CURRENT_DIR + "configure.h.cmake",
    output = "configure.h",
    defines = {
        # these have to be different
        "UTILITY_TEST_DIR": "$(rootpath %s)" % CURRENT_DIR[:-1],
        "UTILITY_BINARY_TEST_DIR": "$(rootpath %s)/write" % CURRENT_DIR[:-1],
    },
    deps = [CURRENT_DIR[:-1]],
    local = True,
)

# depends on containers too, oddly enough
cc_test(
    name = "UtilityAlgorithmsTest",
    srcs = [CURRENT_DIR + "AlgorithmsTest.cpp"],
    local_defines = ["CORRADE_GRACEFUL_ASSERT"],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/Utility:UtilityTestLib",
    ],
)

cc_test(
    name = "UtilityArgumentsTest",
    srcs = [CURRENT_DIR + "ArgumentsTest.cpp"],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/Utility:UtilityTestLib",
    ],
    env = {
        "ARGUMENTSTEST_SIZE": "1337",
        "ARGUMENTSTEST_VERBOSE": "ON",
        "ARGUMENTSTEST_COLOR": "OFF",
        "ARGUMENTSTEST_UNICODE": "hýždě",
    },
)

cc_library(
    name = "AssertTestObjects",
    srcs = [CURRENT_DIR + "AssertTest.cpp"],
    testonly = True,
    deps = ["@corrade//:TestSuite"],
)


cc_test(
    name = "UtilityAssertTest",
    srcs = ["@corrade_src//:src/dummy.cpp"],
    deps = [
        "@corrade//:TestSuite",
        ":AssertTestObjects",
    ],
)

cc_test(
    name = "UtilityAssertStandardTest",
    srcs = [CURRENT_DIR + "AssertTest.cpp"],
    deps = ["@corrade//:TestSuite"],
    local_defines = [
        "CORRADE_STANDARD_ASSERT",
    ],
)

cc_test(
    name = "UtilityAssertStandardDisabledTest",
    srcs = [CURRENT_DIR + "AssertDisabledTest.cpp"],
    deps = ["@corrade//:TestSuite"],
    local_defines = [
        "CORRADE_STANDARD_ASSERT",
        "NDEBUG",
    ],
)

[cc_test(
    name = "Utility%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = ["@corrade//:TestSuite"],
)
for t in [
    "AssertDisabledTest",
    "AssertGracefulTest",
    "EndiannessTest",
    "MurmurHash2Test",
    "HashDigestTest",
    "Sha1Test",
    "StlForwardArrayTest",
    "StlForwardStringTest",
    "StlForwardTupleTest",
    "StlForwardVectorTest",
    "SystemTest",
    "TweakableParserTest",
    # TODO: potentially selectable
    "StlMathTest",
]]

[cc_test(
    name = "Utility%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = ["@corrade//:TestSuite"],
    # TODO: selectable
    linkopts = ["-pthread"],
    # this is emscripten specific feature enable
    features = ["use_pthreads"],
)
for t in [
    "DebugTest",
    "MacrosTest",
]]

[cc_test(
    name = "Utility%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/Utility:UtilityTestLib",
        ":configure",
    ],
)
for t in [
    "FormatTest",
    "StringTest",
    "UnicodeTest",
]]

cc_test(
    name = "UtilityTypeTraitsTest",
    srcs = [
        CURRENT_DIR + "TypeTraitsTest.cpp",
        "@corrade_src//:src/Corrade/Containers/LinkedList.h",
    ],
    deps = ["@corrade//:TestSuite"],
)

# NOTE: reports not sandboxed, whereas bazel actually runs it sandboxed.
# meaning goes wrong in a bunch of places - writing to root, finding rc, etc.
cc_test(
    name = "UtilityDirectoryTest",
    srcs = [CURRENT_DIR + "DirectoryTest.cpp"],
    deps = [
        "@corrade//:TestSuite",
        ":configure",
    ],
    data = [
        CURRENT_DIR + "DirectoryTestFiles/dir/dummy",
        CURRENT_DIR + "DirectoryTestFiles/file",
        CURRENT_DIR + "DirectoryTestFilesUtf8/šňůra/dummy",
        CURRENT_DIR + "DirectoryTestFilesUtf8/hýždě",
    ],
)

# NOTE: interestingly enough, fails with UtilityTestLib linkstatic=False
cc_test(
    name = "UtilityConfigurationTest",
    srcs = [CURRENT_DIR + "ConfigurationTest.cpp"],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/Utility:UtilityTestLib",
        ":configure",
    ],
    data = [
        CURRENT_DIR + "ConfigurationTestFiles/bom.conf",
        CURRENT_DIR + "ConfigurationTestFiles/comments.conf",
        CURRENT_DIR + "ConfigurationTestFiles/comments-saved.conf",
        CURRENT_DIR + "ConfigurationTestFiles/eol-mixed.conf",
        CURRENT_DIR + "ConfigurationTestFiles/eol-unix.conf",
        CURRENT_DIR + "ConfigurationTestFiles/eol-windows.conf",
        CURRENT_DIR + "ConfigurationTestFiles/hierarchic.conf",
        CURRENT_DIR + "ConfigurationTestFiles/hierarchic-empty-group.conf",
        CURRENT_DIR + "ConfigurationTestFiles/hierarchic-empty-subgroup.conf",
        CURRENT_DIR + "ConfigurationTestFiles/hierarchic-missing-bracket.conf",
        CURRENT_DIR + "ConfigurationTestFiles/hierarchic-modified.conf",
        CURRENT_DIR + "ConfigurationTestFiles/hierarchic-shortcuts.conf",
        CURRENT_DIR + "ConfigurationTestFiles/hierarchic-shortcuts-modified.conf",
        CURRENT_DIR + "ConfigurationTestFiles/hýždě.conf",
        CURRENT_DIR + "ConfigurationTestFiles/missing-equals.conf",
        CURRENT_DIR + "ConfigurationTestFiles/missing-quote.conf",
        CURRENT_DIR + "ConfigurationTestFiles/missing-multiline-quote.conf",
        CURRENT_DIR + "ConfigurationTestFiles/multiLine.conf",
        CURRENT_DIR + "ConfigurationTestFiles/multiLine-crlf.conf",
        CURRENT_DIR + "ConfigurationTestFiles/multiLine-crlf-saved.conf",
        CURRENT_DIR + "ConfigurationTestFiles/multiLine-saved.conf",
        CURRENT_DIR + "ConfigurationTestFiles/parse.conf",
        CURRENT_DIR + "ConfigurationTestFiles/parse-modified.conf",
        CURRENT_DIR + "ConfigurationTestFiles/whitespaces.conf",
        CURRENT_DIR + "ConfigurationTestFiles/whitespaces-saved.conf",
    ],
)

corrade_resource(
    name = "ResourceTestData",
    conf = CURRENT_DIR + "ResourceTestFiles/resources.conf",
    deps = [
        CURRENT_DIR + "ResourceTestFiles/predisposition.bin",
        CURRENT_DIR + "ResourceTestFiles/consequence.bin",
    ],
)

corrade_resource(
    name = "ResourceTestEmptyFileData",
    conf = CURRENT_DIR + "ResourceTestFiles/resources-empty-file.conf",
    deps = [
        CURRENT_DIR + "ResourceTestFiles/empty.bin",
    ],
)

corrade_resource(
    name = "ResourceTestNothingData",
    conf = CURRENT_DIR + "ResourceTestFiles/resources-nothing.conf",
    deps = [],
)

cc_test(
    name = "UtilityResourceTest",
    srcs = [
        CURRENT_DIR + "ResourceTest.cpp",
        ":ResourceTestData",
        ":ResourceTestEmptyFileData",
        ":ResourceTestNothingData",
    ],
    data = [
        CURRENT_DIR + "ResourceTestFiles/compiled.cpp",
        CURRENT_DIR + "ResourceTestFiles/compiled-empty.cpp",
        CURRENT_DIR + "ResourceTestFiles/compiled-nothing.cpp",
        CURRENT_DIR + "ResourceTestFiles/compiled-unicode.cpp",
        CURRENT_DIR + "ResourceTestFiles/consequence.bin",
        CURRENT_DIR + "ResourceTestFiles/consequence2.txt",
        CURRENT_DIR + "ResourceTestFiles/empty.bin",
        CURRENT_DIR + "ResourceTestFiles/hýždě.bin",
        CURRENT_DIR + "ResourceTestFiles/hýždě.conf",
        CURRENT_DIR + "ResourceTestFiles/predisposition.bin",
        CURRENT_DIR + "ResourceTestFiles/predisposition2.txt",
        CURRENT_DIR + "ResourceTestFiles/resources.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-empty-alias.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-empty-file.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-empty-filename.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-empty-group.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-no-group.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-nonexistent.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-nothing.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-overriden.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-overriden-different.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-overriden-none.conf",
        CURRENT_DIR + "ResourceTestFiles/resources-overriden-nonexistent-file.conf",
    ],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/Utility:UtilityTestLib",
        ":configure",
    ],
)

cc_library(
    name = "ResourceTestDataLib",
    srcs = [
        ":ResourceTestData",
        ":ResourceTestNothingData",
    ],
    deps = ["@corrade//:Utility"],
    linkstatic = True,
    local_defines = [
        "CORRADE_AUTOMATIC_INITIALIZER=CORRADE_NOOP",
        "CORRADE_AUTOMATIC_FINALIZER=CORRADE_NOOP",
    ],
)

cc_test(
    name = "UtilityResourceStaticTest",
    srcs = [CURRENT_DIR + "ResourceStaticTest.cpp"],
    data = [
        CURRENT_DIR + "ResourceTestFiles/consequence.bin",
        CURRENT_DIR + "ResourceTestFiles/predisposition.bin",
    ],
    deps = [
        "@corrade//:TestSuite",
        ":ResourceTestDataLib",
        ":configure",
    ],
)

# this one is tricky because bazel doesn't deal in shared libraries easily
# NOTE: cc_binary with linkshared=True is a shared object but with one caveat:
# it does not link automatically, have to include it manually in srcs
cc_binary(
    name = "UtilityGlobalStateAcrossLibrariesLibrary",
    srcs = [
        CURRENT_DIR + "GlobalStateAcrossLibrariesLibrary.cpp",
        CURRENT_DIR + "GlobalStateAcrossLibrariesLibrary.h",
        ":ResourceTestData",
    ],
    deps = [
        "@corrade//:Utility",
    ],
    linkshared = True,
)

# pretty sure this one is false positive
#cc_test(
#    name = "UtilityGlobalStateAcrossLibrariesTest",
#    srcs = [
#        "GlobalStateAcrossLibrariesTest.cpp",
#        "GlobalStateAcrossLibrariesLibrary.h",
#        ":UtilityGlobalStateAcrossLibrariesLibrary",
#    ],
#    deps = ["@corrade//:TestSuite"],
#)

# TODO: unix only
cc_test(
    name = "UtilityFileWatcherTest",
    srcs = [CURRENT_DIR + "FileWatcherTest.cpp"],
    deps = [
        "@corrade//:TestSuite",
        ":configure",
    ],
)

cc_test(
    name = "UtilityTweakableTest",
    srcs = [CURRENT_DIR + "TweakableTest.cpp"],
    deps = ["@corrade//:TestSuite"],
)

cc_test(
    name = "UtilityTweakableIntegrationTest",
    srcs = [CURRENT_DIR + "TweakableIntegrationTest.cpp"],
    deps = [
        "@corrade//:TestSuite",
        ":configure",
    ],
    data = [CURRENT_DIR + "TweakableIntegrationTest.cpp"],
)

# TODO: "ConfigurationValueTest"

[[wasm_cc_binary(
    name = "%s_wasm" % t,
    cc_target = ":Utility%s" % t,
    testonly = True,
  ),
  nodejs_test(
    name = "Emscripten_%s" % t,
    data = [":%s_wasm" % t],
    entry_point = ":%s_wasm/Utility%s.js" % (t, t),
  )]
for t in [
    "AlgorithmsTest",
    #"ArgumentsTest",
    "AssertTest",
    "AssertDisabledTest",
    "AssertStandardDisabledTest",
    "AssertGracefulTest",
    "EndiannessTest",
    "MurmurHash2Test",
    #"ConfigurationTest",
    # NOTE: requires pthreads
    #"DebugTest",
    #"MacrosTest",
    "FormatTest",
    "HashDigestTest",
    "Sha1Test",
    "StlForwardArrayTest",
    "StlForwardStringTest",
    "StlForwardTupleTest",
    "StlForwardVectorTest",
    "StlMathTest",
    "StringTest",
    "SystemTest",
    "TweakableParserTest",
    "TypeTraitsTest",
    "UnicodeTest",
]]

[[wasm_cc_binary(
    name = "%s_wasm" % t,
    cc_target = ":Utility%s" % t,
    testonly = True,
  ),
  nodejs_test(
    name = "Emscripten_%s" % t,
    data = [":%s_wasm" % t],
    entry_point = ":%s_wasm/Utility%s.js" % (t, t),
    env = {
        "ARGUMENTSTEST_SIZE": "1337",
        "ARGUMENTSTEST_VERBOSE": "ON",
        "ARGUMENTSTEST_COLOR": "OFF",
        "ARGUMENTSTEST_UNICODE": "hýždě",
    },
  )]
for t in [
    "ArgumentsTest",
]]
