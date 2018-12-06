# Copyright 2017-present The Material Motion Authors. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
# Description:
# A Motion Animator creates performant, interruptible animations from motion specs.

load("@build_bazel_rules_apple//apple:ios.bzl", "ios_ui_test")
load("@build_bazel_rules_swift//swift:swift.bzl", "swift_library")
load("@bazel_ios_warnings//:strict_warnings_objc_library.bzl", "strict_warnings_objc_library")

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

strict_warnings_objc_library(
    name = "MotionAnimator",
    srcs = glob([
        "src/*.m",
        "src/private/*.m",
    ]),
    hdrs = glob([
        "src/*.h",
        "src/private/*.h",
    ]),
    sdk_frameworks = [
        "CoreGraphics",
        "Foundation",
        "QuartzCore",
    ],
    defines = ["IS_BAZEL_BUILD"],
    deps = [
      "@motion_interchange_objc//:MotionInterchange"
    ],
    enable_modules = 1,
    includes = ["src"],
    visibility = ["//visibility:public"],
)

swift_library(
    name = "UnitTestsSwiftLib",
    srcs = glob([
        "tests/unit/*.swift",
    ]),
    defines = ["IS_BAZEL_BUILD"],
    deps = [":MotionAnimator"],
    visibility = ["//visibility:private"],
)

objc_library(
    name = "UnitTestsLib",
    srcs = glob([
        "tests/unit/*.m",
    ]),
    hdrs = glob([
        "tests/unit/*.h",
    ]),
    enable_modules = 1,
    deps = [":MotionAnimator"],
    visibility = ["//visibility:private"],
)

ios_ui_test(
    name = "UnitTests",
    deps = [
      ":UnitTestsLib",
      ":UnitTestsSwiftLib"
    ],
    test_host = "@build_bazel_rules_apple//apple/testing/default_host/ios",
    minimum_os_version = "8.0",
    timeout = "short",
    visibility = ["//visibility:private"],
)
