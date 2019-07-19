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



rust_library(
    name = "wasm_bindgen_macro",
    crate_root = "src/lib.rs",
    crate_type = "proc-macro",
    edition = "2015",
    srcs = glob(["**/*.rs"]),
    deps = [
        "@raze__quote__0_6_12//:quote",
        "@raze__wasm_bindgen_macro_support__0_2_40//:wasm_bindgen_macro_support",
    ],
    rustc_flags = [
        "--cap-lints=allow",
    ],
    version = "0.2.40",
    crate_features = [
        "spans",
        "wasm-bindgen-macro-support",
    ],
)
