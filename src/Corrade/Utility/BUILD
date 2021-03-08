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

CURRENT_DIR = "@corrade_src//:src/Corrade/Utility/"
CONTAINERS_DIR = "@corrade_src//:src/Corrade/Containers/"

cc_library(
    name = "headers",
    hdrs = [
        CURRENT_DIR + "Algorithms.h",
        CURRENT_DIR + "Arguments.h",
        CURRENT_DIR + "AbstractHash.h",
        CURRENT_DIR + "Assert.h",
        CURRENT_DIR + "Configuration.h",
        CURRENT_DIR + "ConfigurationGroup.h",
        CURRENT_DIR + "ConfigurationValue.h",
        CURRENT_DIR + "Debug.h",
        CURRENT_DIR + "DebugStl.h",
        CURRENT_DIR + "Directory.h",
        CURRENT_DIR + "Endianness.h",
        CURRENT_DIR + "EndiannessBatch.h",
        CURRENT_DIR + "Format.h",
        CURRENT_DIR + "FormatStl.h",
        CURRENT_DIR + "Macros.h",
        CURRENT_DIR + "MurmurHash2.h",
        CURRENT_DIR + "Resource.h",
        CURRENT_DIR + "Sha1.h",
        CURRENT_DIR + "String.h",
        CURRENT_DIR + "StlForwardArray.h",
        CURRENT_DIR + "StlForwardString.h",
        CURRENT_DIR + "StlForwardTuple.h",
        CURRENT_DIR + "StlForwardVector.h",
        CURRENT_DIR + "StlMath.h",
        CURRENT_DIR + "System.h",
        CURRENT_DIR + "TypeTraits.h",
        CURRENT_DIR + "Unicode.h",
        CURRENT_DIR + "utilities.h",
        CURRENT_DIR + "Utility.h",
        CURRENT_DIR + "visibility.h",
        CURRENT_DIR + "VisibilityMacros.h",
        # TODO: this is selectable
        CURRENT_DIR + "FileWatcher.h",
        CURRENT_DIR + "Tweakable.h",
        CURRENT_DIR + "TweakableParser.h",
    ],
    deps = [
        "@corrade//:Main",
        "//src/Corrade/Containers:headers",
    ],
    visibility = ["//src/Corrade:__subpackages__"]
)

cc_library(
    name = "Utility",
    srcs = [
        CURRENT_DIR + "Debug.cpp",
        CURRENT_DIR + "Directory.cpp",
        CURRENT_DIR + "Configuration.cpp",
        CURRENT_DIR + "ConfigurationValue.cpp",
        CURRENT_DIR + "MurmurHash2.cpp",
        CURRENT_DIR + "Sha1.cpp",
        CURRENT_DIR + "System.cpp",
        # GRACEFUL ASSERT
        CURRENT_DIR + "Algorithms.cpp",
        CURRENT_DIR + "Arguments.cpp",
        CURRENT_DIR + "ConfigurationGroup.cpp",
        CURRENT_DIR + "Format.cpp",
        CURRENT_DIR + "Resource.cpp",
        CURRENT_DIR + "Implementation/Resource.h",
        CURRENT_DIR + "String.cpp",
        CURRENT_DIR + "Unicode.cpp",
        CONTAINERS_DIR + "ArrayTuple.cpp",
        CONTAINERS_DIR + "String.cpp",
        CONTAINERS_DIR + "StringView.cpp",
        # TODO: this is selectable
        CURRENT_DIR + "FileWatcher.cpp",
        CURRENT_DIR + "Tweakable.cpp",
        CURRENT_DIR + "Implementation/tweakable.h",
        CURRENT_DIR + "TweakableParser.cpp",
    ],
    # TODO: this is selectable
    linkopts = ["-ldl"],
    deps = [":headers"],
)

cc_library(
    name = "UtilityTestLib",
    srcs = [
        CURRENT_DIR + "Algorithms.cpp",
        CURRENT_DIR + "Arguments.cpp",
        CURRENT_DIR + "ConfigurationGroup.cpp",
        CURRENT_DIR + "Format.cpp",
        CURRENT_DIR + "Resource.cpp",
        CURRENT_DIR + "Implementation/Resource.h",
        CURRENT_DIR + "String.cpp",
        CURRENT_DIR + "Unicode.cpp",
        CONTAINERS_DIR + "ArrayTuple.cpp",
        CONTAINERS_DIR + "String.cpp",
        CONTAINERS_DIR + "StringView.cpp",
    ],
    deps = [":Utility"],
    local_defines = ["CORRADE_GRACEFUL_ASSERT"],
    testonly = True,
    visibility = ["//src/Corrade:__subpackages__"],
)


cc_binary(
    name = "corrade-rc",
    srcs = [CURRENT_DIR + "rc.cpp"],
    linkstatic = True,
    deps = [":Utility"],
)
