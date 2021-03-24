# Copyright 2021 The Bazel Authors. All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http:#www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load("@rules_cc//cc:defs.bzl", "cc_library")
load("@rules_perl//perl:perl.bzl", "perl_binary", "perl_library", "perl_xs")

perl_library(
    name = "CacheMemcachedFast",
    srcs = [
        "lib/Cache/Memcached/Fast.pm",
        ":CacheMemcachedFastXS",
    ],
    visibility = ["//visibility:public"],
)

perl_binary(
    name = "gencrc32_script",
    srcs = ["src/gencrc32.pl"],
)

genrule(
    name = "compute_crc32",
    outs = [
        "src/compute_crc32.c",
        "src/compute_crc32.h",
    ],
    cmd = "$(location :gencrc32_script) $(location src/compute_crc32.c) $(location src/compute_crc32.h)",
    tools = [":gencrc32_script"],
)

perl_binary(
    name = "genparser_script",
    srcs = ["src/genparser.pl"],
)

genrule(
    name = "parse_keyword",
    srcs = ["src/reply.kw"],
    outs = [
        "src/parse_keyword.c",
        "src/parse_keyword.h",
    ],
    cmd = "$(location :genparser_script) $< $(location src/parse_keyword.c) $(location src/parse_keyword.h)",
    tools = [":genparser_script"],
)

perl_xs(
    name = "CacheMemcachedFastXS",
    srcs = ["Fast.xs"],
    defines = [
        "VERSION=\"0.26\"",
        "XS_VERSION=\"0.26\"",
    ],
    output_loc = "arch/auto/Cache/Memcached/Fast/Fast.so",
    textual_hdrs = ["ppport.h"],
    typemaps = ["typemap"],
    deps = [":libclient"],
)

cc_library(
    name = "libclient",
    srcs = [
        "src/array.c",
        "src/array.h",
        "src/client.c",
        "src/compute_crc32.c",
        "src/compute_crc32.h",
        "src/connect.c",
        "src/connect.h",
        "src/dispatch_key.c",
        "src/dispatch_key.h",
        "src/parse_keyword.c",
        "src/parse_keyword.h",
        "src/socket_posix.c",
        "src/socket_posix.h",
    ],
    hdrs = [
        "src/client.h",
    ],
    copts = ["-I."],
    defines = [
        "HAVE_POLL_H",
    ],
    includes = [
        ".",
        "src",
    ],
)
