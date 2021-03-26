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
load(
    "@corrade//:index.bzl",
    "corrade_configure_header",
    "corrade_static_plugin",
    "corrade_dynamic_plugin",
)
load("@emsdk//emscripten_toolchain:wasm_rules.bzl", "wasm_cc_binary")
load("@build_bazel_rules_nodejs//:index.bzl", "nodejs_test")

CURRENT_DIR = "@corrade_src//:src/Corrade/PluginManager/Test/"

corrade_configure_header(
    name = "configure",
    src = CURRENT_DIR + "configure.h.cmake",
    output = "configure.h",
    defines = {
        "PLUGINS_DIR": "plugins",
        "DOG_PLUGIN_FILENAME": "$(rootpath :Dog)",
        "DOGGO_PLUGIN_FILENAME": "$(rootpath :Doggo)",
        "PITBULL_PLUGIN_FILENAME": "$(rootpath :PitBull)",
    },
    deps = [
        ":Dog",
        ":Doggo",
        ":PitBull",
    ],
    local = True,
)


corrade_static_plugin(
    name = "CustomSuffixStatic",
    metadata_file = CURRENT_DIR + "custom-suffix/CustomSuffixStatic.modconf",
    srcs = [
        CURRENT_DIR + "custom-suffix/CustomSuffixStatic.cpp",
        "//src/Corrade/PluginManager:PluginManagerTestLib",
    ],
    hdrs = [
        CURRENT_DIR + "AbstractCustomSuffix.h",
    ],
)

corrade_static_plugin(
    name = "DisabledMetadataStatic",
    srcs = [
        CURRENT_DIR + "disabled-metadata/DisabledMetadataStatic.cpp",
        "//src/Corrade/PluginManager:PluginManagerTestLib",
    ],
    hdrs = [
        CURRENT_DIR + "AbstractDisabledMetadata.h",
    ],
)

corrade_static_plugin(
    name = "Canary",
    metadata_file = CURRENT_DIR + "animals/Canary.conf",
    srcs = [
        CURRENT_DIR + "animals/Canary.cpp",
        "//src/Corrade/PluginManager:PluginManagerTestLib",
    ],
    hdrs = [
        CURRENT_DIR + "animals/Canary.h",
        CURRENT_DIR + "AbstractAnimal.h",
    ],
    copts = ["-fPIC"],
)

corrade_static_plugin(
    name = "Dird",
    metadata_file = CURRENT_DIR + "animals/Dird.conf",
    srcs = [
        CURRENT_DIR + "animals/Dird.cpp",
        "//src/Corrade/PluginManager:PluginManagerTestLib",
    ],
    hdrs = [
        CURRENT_DIR + "AbstractAnimal.h",
    ],
)

corrade_static_plugin(
    name = "InitFiniStatic",
    metadata_file = CURRENT_DIR + "dummy.conf",
    srcs = [
        CURRENT_DIR + "init-fini/InitFiniStatic.cpp",
    ],
    hdrs = [
        CURRENT_DIR + "init-fini/InitFiniStatic.h",
        CURRENT_DIR + "init-fini/InitFini.h",
    ],
    deps = [
        ":configure",
    ],
)

[corrade_dynamic_plugin(
    name = "%s" % dog,
    metadata_file = CURRENT_DIR + "animals/%s.conf" % dog,
    subdir = "plugins/animals",
    srcs = [
        CURRENT_DIR + "animals/%s.cpp" % dog,
        CURRENT_DIR + "animals/Dog.h",
        CURRENT_DIR + "AbstractAnimal.h",
    ],
    deps = ["//src/Corrade/PluginManager:PluginManagerTestLib"],
)
for dog in [
    "Dog",
    "Bulldog",
    "PitBull",
]]

corrade_dynamic_plugin(
    name = "Snail",
    metadata_file = CURRENT_DIR + "animals/Snail.conf",
    subdir = "plugins/animals",
    srcs = [
        CURRENT_DIR + "animals/Snail.cpp",
        CURRENT_DIR + "AbstractAnimal.h",
    ],
    deps = ["//src/Corrade/PluginManager:PluginManagerTestLib"],
)

corrade_dynamic_plugin(
    name = "CustomSuffix",
    metadata_file = CURRENT_DIR + "custom-suffix/CustomSuffix.modconf",
    subdir = "plugins/custom-suffix",
    srcs = [
        CURRENT_DIR + "custom-suffix/CustomSuffix.cpp",
        CURRENT_DIR + "AbstractCustomSuffix.h",
    ],
    override_suffix = "mod",
)

corrade_dynamic_plugin(
    name = "Deletable",
    metadata_file = CURRENT_DIR + "deletable/Deletable.conf",
    subdir = "plugins/deletable",
    srcs = [
        CURRENT_DIR + "deletable/Deletable.cpp",
        CURRENT_DIR + "AbstractDeletable.h",
    ],
)

corrade_dynamic_plugin(
    name = "DisabledMetadata",
    subdir = "plugins/disabled-metadata",
    srcs = [
        CURRENT_DIR + "disabled-metadata/DisabledMetadata.cpp",
        CURRENT_DIR + "AbstractDisabledMetadata.h",
    ],
)

corrade_dynamic_plugin(
    name = "Doggo",
    metadata_file = CURRENT_DIR + "doggo/Doggo.conf",
    subdir = "plugins/doggo",
    srcs = [
        CURRENT_DIR + "doggo/Doggo.cpp",
        CURRENT_DIR + "AbstractAnimal.h",
    ],
    deps = ["//src/Corrade/PluginManager:PluginManagerTestLib"],
)

[corrade_dynamic_plugin(
    name = "%s" % food,
    metadata_file = CURRENT_DIR + "food/%s.conf" % food,
    subdir = "plugins/food",
    srcs = [
        CURRENT_DIR + "food/HotDog.cpp",
        CURRENT_DIR + "animals/Dog.h",
        CURRENT_DIR + "AbstractAnimal.h",
        CURRENT_DIR + "AbstractFood.h",
    ],
    deps = ["//src/Corrade/PluginManager:PluginManagerTestLib"],
)
for food in [
    "HotDog",
    "HotDogWithSnail",
]]

[corrade_dynamic_plugin(
    name = "%s" % food,
    metadata_file = CURRENT_DIR + "food/%s.conf" % food,
    subdir = "plugins/food",
    srcs = [
        CURRENT_DIR + "food/%s.cpp" % food,
        CURRENT_DIR + "AbstractFood.h",
    ],
    deps = ["//src/Corrade/PluginManager:PluginManagerTestLib"],
)
for food in [
    "OldBread",
    "RottenTomato",
]]

corrade_dynamic_plugin(
    name = "InitFiniDynamic",
    metadata_file = CURRENT_DIR + "init-fini/InitFiniDynamic.conf",
    subdir = "plugins/init-fini",
    srcs = [
        CURRENT_DIR + "init-fini/InitFiniDynamic.cpp",
        CURRENT_DIR + "init-fini/InitFini.h",
        CURRENT_DIR + "init-fini/InitFiniStatic.h",
    ],
    deps = [
        "@corrade//:PluginManager",
        ":configure",
    ]
)

corrade_dynamic_plugin(
    name = "WrongMetadata",
    metadata_file = CURRENT_DIR + "wrong-metadata/WrongMetadata.conf",
    subdir = "plugins/wrong-metadata",
    srcs = [
        CURRENT_DIR + "wrong-metadata/WrongMetadata.cpp",
        CURRENT_DIR + "wrong-metadata/WrongMetadata.h",
    ],
    deps = [
        ":configure",
    ]
)

[corrade_dynamic_plugin(
    name = "%s" % wrong,
    metadata_file = CURRENT_DIR + "dummy.conf",
    subdir = "plugins/wrong",
    srcs = [
        CURRENT_DIR + "wrong/%s.cpp" % wrong,
    ],
)
for wrong in [
    "NoPluginFinalizer",
    "NoPluginInitializer",
    "NoPluginInstancer",
    "NoPluginInterface",
    "NoPluginVersion",
]]

corrade_dynamic_plugin(
    name = "UnresolvedReference",
    metadata_file = CURRENT_DIR + "dummy.conf",
    subdir = "plugins/wrong",
    srcs = [
        CURRENT_DIR + "wrong/UnresolvedReference.cpp",
    ],
    deps = ["//src/Corrade/Interconnect:headers"],
)

# NOTE: fails with bazel atm so set to manual
cc_test(
    name = "PluginManagerManagerTest",
    srcs = [
        CURRENT_DIR + "ManagerTest.cpp",
        CURRENT_DIR + "AbstractAnimal.cpp",
        CURRENT_DIR + "AbstractCustomSuffix.cpp",
        CURRENT_DIR + "AbstractDeletable.cpp",
        CURRENT_DIR + "AbstractDisabledMetadata.cpp",
        CURRENT_DIR + "AbstractFood.cpp",
        CURRENT_DIR + "AbstractAnimal.h",
        CURRENT_DIR + "AbstractCustomSuffix.h",
        CURRENT_DIR + "AbstractDeletable.h",
        CURRENT_DIR + "AbstractDisabledMetadata.h",
        CURRENT_DIR + "AbstractFood.h",
        CURRENT_DIR + "wrong-metadata/WrongMetadata.h",
    ],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/PluginManager:PluginManagerTestLib",
        ":Canary",
        ":CustomSuffixStatic",
        ":DisabledMetadataStatic",
        ":configure",
    ],
    data = [
        ":Dog",
        ":Bulldog",
        ":PitBull",
        ":Snail",
        ":CustomSuffix",
        ":Deletable",
        ":DisabledMetadata",
        ":Doggo",
        ":HotDog",
        ":HotDogWithSnail",
        ":OldBread",
        ":RottenTomato",
        ":InitFiniDynamic",
        ":WrongMetadata",
        ":NoPluginFinalizer",
        ":NoPluginInitializer",
        ":NoPluginInstancer",
        ":NoPluginInterface",
        ":NoPluginVersion",
        ":UnresolvedReference",
    ],
    tags = ["manual"],
)

cc_test(
    name = "PluginManagerManagerInitFiniTest",
    srcs = [CURRENT_DIR + "ManagerInitFiniTest.cpp"],
    deps = [
        "@corrade//:TestSuite",
        "@corrade//:PluginManager",
        ":InitFiniStatic",
    ],
    data = [
        ":InitFiniDynamic",
    ],
)

cc_test(
    name = "PluginManagerImportStaticTest",
    srcs = [
        CURRENT_DIR + "ImportStaticTest.cpp",
        CURRENT_DIR + "AbstractAnimal.cpp",
        CURRENT_DIR + "AbstractAnimal.h",
    ],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/PluginManager:PluginManagerTestLib",
        ":Canary",
        ":Dird",
        ":configure",
    ],
)

cc_test(
    name = "PluginManagerAbstractPluginTest",
    srcs = [
        CURRENT_DIR + "AbstractPluginTest.cpp",
        CURRENT_DIR + "AbstractAnimal.cpp",
        CURRENT_DIR + "AbstractAnimal.h",
    ],
    deps = [
        "@corrade//:TestSuite",
        "//src/Corrade/PluginManager:PluginManagerTestLib",
        ":Canary",
        ":configure",
    ],
)

# this one is tricky because bazel doesn't deal in shared libraries easily
# NOTE: cc_binary with linkshared=True is a shared object but with one caveat:
# it does not link automatically, have to include it manually in srcs
cc_library(
    name = "PluginManagerGlobalStateAcrossLibrariesLibrary",
    srcs = [
        CURRENT_DIR + "GlobalStateAcrossLibrariesLibrary.cpp",
        CURRENT_DIR + "GlobalStateAcrossLibrariesLibrary.h",
        CURRENT_DIR + "AbstractAnimal.h",
        ":configure",
        ":Canary",
    ],
    deps = [
        "//src/Corrade/PluginManager:PluginManagerTestLib",
        ":configure",
    ],
)

# TODO: platform compatibility
#cc_test(
#    name = "PluginManagerGlobalStateAcrossLi___Test",
#    srcs = [
#        "GlobalStateAcrossLibrariesTest.cpp",
#        "GlobalStateAcrossLibrariesLibrary.h",
#        "AbstractAnimal.cpp",
#        "AbstractAnimal.h",
#    ],
#    deps = [
#        ":PluginManagerGlobalStateAcrossLibrariesLibrary",
#        "@corrade//:TestSuite",
#        "//src/Corrade/PluginManager:PluginManagerTestLib",
#        ":configure",
#    ],
#)

[[wasm_cc_binary(
    name = "%s_wasm" % t,
    cc_target = ":PluginManager%s" % t,
    testonly = True,
  ),
  nodejs_test(
    name = "Emscripten_%s" % t,
    data = [":%s_wasm" % t],
    entry_point = ":%s_wasm/PluginManager%s.js" % (t, t),
  )]
for t in [
    "ManagerTest",
    "ManagerInitFiniTest",
    "ImportStaticTest",
    "AbstractPluginTest",
]]
