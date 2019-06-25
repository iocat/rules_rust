load("@bazel_skylib//:bzl_library.bzl", "bzl_library")

package(default_visibility = ["//visibility:public"])

exports_files([
    "known_shas.bzl",
    "repositories.bzl",
    "rust.bzl",
    "toolchain.bzl",
])

toolchain_type(
    name = "toolchain",
)

toolchain_type(
    name = "wasm_toolchain",
)

bzl_library(
    name = "rules",
    srcs = glob(["**/*.bzl"]),
)
