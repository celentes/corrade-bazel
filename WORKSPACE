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
workspace(name = "corrade")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# Toolchains for docker-sandbox build
http_archive(
    name = "bazel_toolchains",
    sha256 = "1adf5db506a7e3c465a26988514cfc3971af6d5b3c2218925cd6e71ee443fc3f",
    strip_prefix = "bazel-toolchains-4.0.0",
    urls = [
        "https://github.com/bazelbuild/bazel-toolchains/releases/download/4.0.0/bazel-toolchains-4.0.0.tar.gz",
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-toolchains/releases/download/4.0.0/bazel-toolchains-4.0.0.tar.gz",
    ],
)

http_archive(
    name = "build_bazel_rules_nodejs",
    sha256 = "dd7ea7efda7655c218ca707f55c3e1b9c68055a70c31a98f264b3445bc8f4cb1",
    urls = ["https://github.com/bazelbuild/rules_nodejs/releases/download/3.2.3/rules_nodejs-3.2.3.tar.gz"],
)

load("@bazel_toolchains//rules:rbe_repo.bzl", "rbe_autoconfig")
rbe_autoconfig(
    name = "rbe_ubuntu1804",
    env = {
        "ABI_LIBC_VERSION": "glibc_2.27",
        "ABI_VERSION": "clang",
        "BAZEL_COMPILER": "clang",
        "BAZEL_HOST_SYSTEM": "i686-unknown-linux-gnu",
        "BAZEL_TARGET_CPU": "k8",
        "BAZEL_TARGET_LIBC": "glibc_2.27",
        "BAZEL_TARGET_SYSTEM": "x86_64-unknown-linux-gnu",
        "CC": "clang",
        "CXX": "clang++",
        "CC_TOOLCHAIN_NAME": "linux_gnu_x86",
    },
    registry = "l.gcr.io",
    repository = "google/rbe-ubuntu18-04",
    digest = "sha256:48b67b41118dbcdfc265e7335f454fbefa62681ab8d47200971fc7a52fb32054",
)

all_exports = """exports_files(glob(["**"], exclude_directories=0), visibility = ["//visibility:public"])"""
http_archive(
    name = "corrade_src",
    url = "https://github.com/mosra/corrade/archive/6054f1b1d3f768afc226bb0f633b8216283e2158.tar.gz",
    sha256 = "d02bee8c8c7f4249201d6a122e5efb7c69b898d1ece8a1e252416e3154035160",
    strip_prefix = "corrade-6054f1b1d3f768afc226bb0f633b8216283e2158",
    build_file_content = all_exports,
)

http_archive(
    name = "emsdk",
    strip_prefix = "emsdk-c1589b55641787d55d53e883852035beea9aec3f/bazel",
    url = "https://github.com/emscripten-core/emsdk/archive/c1589b55641787d55d53e883852035beea9aec3f.tar.gz",
    sha256 = "7a58a9996b113d3e0675df30b5f17e28aa47de2e684a844f05394fe2f6f12e8e",
)

load("@emsdk//:deps.bzl", emsdk_deps = "deps")
emsdk_deps()

load("@emsdk//:emscripten_deps.bzl", emsdk_emscripten_deps = "emscripten_deps")
emsdk_emscripten_deps()
