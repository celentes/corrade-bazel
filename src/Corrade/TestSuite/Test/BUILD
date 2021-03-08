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

CURRENT_DIR = "@corrade_src//:src/Corrade/TestSuite/Test/"

corrade_configure_header(
    name = "configure",
    src = CURRENT_DIR + "configure.h.cmake",
    output = "configure.h",
    defines = {
        "RELATIVE_TEST_DIR": "$(rootpath %s)" % CURRENT_DIR[:-1],
        "ABSOLUTE_TEST_DIR": "$(rootpath %s)/BundledFilesTestFiles" % CURRENT_DIR[:-1],
        "TESTER_TEST_DIR": "$(rootpath %s)/TesterTestFiles" % CURRENT_DIR[:-1],
    },
    deps = [CURRENT_DIR[:-1]],
    local = True,
)

cc_test(
    name = "TestSuiteArgumentsTest",
    srcs = [CURRENT_DIR + "ArgumentsTest.cpp"],
    args = [
        "--arguments-value",
        "hello",
    ],
    deps = ["@corrade//:TestSuite"],
)

cc_test(
    name = "TestSuiteTesterTest",
    srcs = [CURRENT_DIR + "TesterTest.cpp"],
    deps = [
        "@corrade//:TestSuite",
        ":configure",
    ],
    data = [
        CURRENT_DIR + "TesterTestFiles/abortOnFail.txt",
        CURRENT_DIR + "TesterTestFiles/abortOnFailSkip.txt",
        CURRENT_DIR + "TesterTestFiles/benchmarkCpuClock.txt",
        CURRENT_DIR + "TesterTestFiles/benchmarkCpuCycles.txt",
        CURRENT_DIR + "TesterTestFiles/benchmarkDiscardAll.txt",
        CURRENT_DIR + "TesterTestFiles/benchmarkWallClock.txt",
        CURRENT_DIR + "TesterTestFiles/benchmarkDebugBuildNote.txt",
        CURRENT_DIR + "TesterTestFiles/benchmarkCpuScalingWarning.txt",
        CURRENT_DIR + "TesterTestFiles/benchmarkCpuScalingWarningVerbose.txt",
        CURRENT_DIR + "TesterTestFiles/compareMessageFailed.txt",
        CURRENT_DIR + "TesterTestFiles/compareMessageVerboseDisabled.txt",
        CURRENT_DIR + "TesterTestFiles/compareMessageVerboseEnabled.txt",
        CURRENT_DIR + "TesterTestFiles/compareMessageXfail.txt",
        CURRENT_DIR + "TesterTestFiles/noCatch.txt",
        CURRENT_DIR + "TesterTestFiles/noXfail.txt",
        CURRENT_DIR + "TesterTestFiles/repeatAll.txt",
        CURRENT_DIR + "TesterTestFiles/repeatEvery.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticAbortOnFail.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticSucceededDisabled.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticSucceededEnabled.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticFailedDisabled.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticFailedEnabled.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticVerboseDisabled.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticVerboseEnabled.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticXfail.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticXpassDisabled.txt",
        CURRENT_DIR + "TesterTestFiles/saveDiagnosticXpassEnabled.txt",
        CURRENT_DIR + "TesterTestFiles/shuffleOne.txt",
        CURRENT_DIR + "TesterTestFiles/skipBenchmarks.txt",
        CURRENT_DIR + "TesterTestFiles/skipOnly.txt",
        CURRENT_DIR + "TesterTestFiles/skipTests.txt",
        CURRENT_DIR + "TesterTestFiles/test.txt",
        CURRENT_DIR + "TesterTestFiles/testName.txt",
        CURRENT_DIR + "TesterTestFiles/cpu-governor-performance.txt",
        CURRENT_DIR + "TesterTestFiles/cpu-governor-powersave.txt",
    ],
)

cc_test(
    name = "TestSuiteBundledFilesTest",
    srcs = [CURRENT_DIR + "BundledFilesTest.cpp"],
    deps = [
        "@corrade//:TestSuite",
        ":configure",
    ],
    data = [
        # bazel has much stricter rules on files location and sourcing
        # so can't do the kind of shenanigans cmake allows doing
        CURRENT_DIR + "BundledFilesTestFiles/a.txt",
        CURRENT_DIR + "BundledFilesTestFiles/b.txt",
        CURRENT_DIR + "BundledFilesTestFiles/c.txt",
        CURRENT_DIR + "BundledFilesTestFiles/d.txt",
    ],
)

[cc_test(
    name = "TestSuite%s" % t,
    srcs = [CURRENT_DIR + "%s.cpp" % t],
    deps = ["@corrade//:TestSuite"],
)
for t in [
    "ComparatorTest",
    "BenchmarkStatsTest",
    # Bazel doesn't know how to expect failing tests
    # TODO: find a way to fix/wrap?
    #"FailingTest",
]]
