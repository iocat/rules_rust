"""
cargo-raze crate build file.

DO NOT EDIT! Replaced on runs of cargo-raze
"""
package(default_visibility = [
  # Public for visibility by "@raze__crate__version//" targets.
  #
  # Prefer access through "//wasm_bindgen/raze", which limits external
  # visibility to explicit Cargo.toml dependencies.
  "//visibility:public",
])

licenses([
  "notice", # "MIT,Apache-2.0"
])

load(
    "@io_bazel_rules_rust//rust:rust.bzl",
    "rust_library",
    "rust_binary",
    "rust_test",
)

rust_binary(
    name = "backtrace_build_script",
    srcs = glob(["**/*.rs"]),
    crate_root = "build.rs",
    edition = "2015",
    deps = [
        "@raze__autocfg__0_1_4//:autocfg",
    ],
    rustc_flags = [
        "--cap-lints=allow",
    ],
    crate_features = [
      "backtrace-sys",
      "dbghelp",
      "default",
      "dladdr",
      "libbacktrace",
      "libunwind",
      "std",
    ],
    data = glob(["*"]),
    version = "0.3.31",
    visibility = ["//visibility:private"],
)

genrule(
    name = "backtrace_build_script_executor",
    srcs = glob(["*", "**/*.rs"]),
    outs = ["backtrace_out_dir_outputs.tar.gz"],
    tools = [
      ":backtrace_build_script",
    ],
    local = 1,
    cmd = "mkdir -p backtrace_out_dir_outputs/;"
        + " (export CARGO_MANIFEST_DIR=\"$$PWD/$$(dirname $(location :Cargo.toml))\";"
        # TODO(acmcarther): This needs to be revisited as part of the cross compilation story.
        #                   See also: https://github.com/google/cargo-raze/pull/54
        + " export TARGET='x86_64-unknown-linux-gnu';"
        + " export RUST_BACKTRACE=1;"
        + " export CARGO_FEATURE_BACKTRACE_SYS=1;"
        + " export CARGO_FEATURE_DBGHELP=1;"
        + " export CARGO_FEATURE_DEFAULT=1;"
        + " export CARGO_FEATURE_DLADDR=1;"
        + " export CARGO_FEATURE_LIBBACKTRACE=1;"
        + " export CARGO_FEATURE_LIBUNWIND=1;"
        + " export CARGO_FEATURE_STD=1;"
        + " export OUT_DIR=$$PWD/backtrace_out_dir_outputs;"
        + " export BINARY_PATH=\"$$PWD/$(location :backtrace_build_script)\";"
        + " export OUT_TAR=$$PWD/$@;"
        + " cd $$(dirname $(location :Cargo.toml)) && $$BINARY_PATH && tar -czf $$OUT_TAR -C $$OUT_DIR .)"
)

# Unsupported target "accuracy" with type "test" omitted
# Unsupported target "backtrace" with type "example" omitted

rust_library(
    name = "backtrace",
    crate_root = "src/lib.rs",
    crate_type = "lib",
    edition = "2015",
    srcs = glob(["**/*.rs"]),
    deps = [
        "@raze__backtrace_sys__0_1_28//:backtrace_sys",
        "@raze__cfg_if__0_1_9//:cfg_if",
        "@raze__libc__0_2_58//:libc",
        "@raze__rustc_demangle__0_1_15//:rustc_demangle",
    ],
    rustc_flags = [
        "--cap-lints=allow",
    ],
    out_dir_tar = ":backtrace_build_script_executor",
    version = "0.3.31",
    crate_features = [
        "backtrace-sys",
        "dbghelp",
        "default",
        "dladdr",
        "libbacktrace",
        "libunwind",
        "std",
    ],
)

# Unsupported target "benchmarks" with type "bench" omitted
# Unsupported target "long_fn_name" with type "test" omitted
# Unsupported target "raw" with type "example" omitted
# Unsupported target "skip_inner_frames" with type "test" omitted
# Unsupported target "smoke" with type "test" omitted
