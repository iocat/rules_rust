workspace(name = "io_bazel_rules_rust")

load(
    "@bazel_tools//tools/build_defs/repo:git.bzl",
    "git_repository",
    "new_git_repository",
)
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

local_repository(
    name = "examples",
    path = "examples",
)

local_repository(
    name = "docs",
    path = "docs",
)

http_archive(
    name = "bazel_skylib",
    sha256 = "eb5c57e4c12e68c0c20bc774bfbc60a568e800d025557bc4ea022c6479acc867",
    strip_prefix = "bazel-skylib-0.6.0",
    url = "https://github.com/bazelbuild/bazel-skylib/archive/0.6.0.tar.gz",
)

# TODO: Move this to examples/WORKSPACE when recursive repositories are enabled.
load("@io_bazel_rules_rust//rust:repositories.bzl", "rust_repositories")
rust_repositories()

new_git_repository(
    name = "libc",
    build_file = "@io_bazel_rules_rust//:libc.BUILD",
    remote = "https://github.com/rust-lang/libc",
    tag = "0.2.20",
)

load("@io_bazel_rules_rust//proto:repositories.bzl", "rust_proto_repositories")
rust_proto_repositories()

load("@io_bazel_rules_rust//bindgen:repositories.bzl", "rust_bindgen_repositories")
rust_bindgen_repositories()

load("@io_bazel_rules_rust//wasm_bindgen:repositories.bzl", "rust_wasm_bindgen_repositories")
rust_wasm_bindgen_repositories()

# Stardoc and its dependencies
http_archive(
    name = "io_bazel_skydoc",
    url = "https://github.com/bazelbuild/skydoc/archive/0a008878383c51c41db24b313980de19996a6438.zip",
    strip_prefix = "skydoc-0a008878383c51c41db24b313980de19996a6438",
)

load("@io_bazel_skydoc//:setup.bzl", "skydoc_repositories")
skydoc_repositories()

load("@io_bazel_rules_sass//:package.bzl", "rules_sass_dependencies")
rules_sass_dependencies()

load("@build_bazel_rules_nodejs//:defs.bzl", "node_repositories", "npm_install")
node_repositories()

# Dependencies for the @examples//hello_world_wasm example.
npm_install(
    name = "npm",
    package_json = "//:package.json",
    package_lock_json = "//:package-lock.json",
)

load("@io_bazel_rules_sass//:defs.bzl", "sass_repositories")
sass_repositories()
# --- end stardoc


http_archive(
    name = "bazel_toolchains",
    sha256 = "5962fe677a43226c409316fcb321d668fc4b7fa97cb1f9ef45e7dc2676097b26",
    strip_prefix = "bazel-toolchains-be10bee3010494721f08a0fccd7f57411a1e773e",
    urls = [
      "https://mirror.bazel.build/github.com/bazelbuild/bazel-toolchains/archive/be10bee3010494721f08a0fccd7f57411a1e773e.tar.gz",
      "https://github.com/bazelbuild/bazel-toolchains/archive/be10bee3010494721f08a0fccd7f57411a1e773e.tar.gz",
    ],
)

load("@bazel_toolchains//rules:rbe_repo.bzl", "rbe_autoconfig")

# Creates toolchain configuration for remote execution with BuildKite CI
# for rbe_ubuntu1604
rbe_autoconfig(
    name = "buildkite_config",
)

load("@io_bazel_rules_rust//:workspace.bzl", "bazel_version")
bazel_version(name = "bazel_version")
