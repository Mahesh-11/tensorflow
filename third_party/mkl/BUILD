licenses(["notice"])  # 3-Clause BSD

load("@bazel_skylib//:bzl_library.bzl", "bzl_library")

config_setting(
    name = "build_with_mkl",
    define_values = {
        "build_with_mkl": "true",
    },
    visibility = ["//visibility:public"],
)

config_setting(
    name = "build_with_mkl_lnx_x64",
    define_values = {
        "build_with_mkl": "true",
    },
    values = {
        "cpu": "k8",
    },
    visibility = ["//visibility:public"],
)

config_setting(
    name = "build_with_mkl_aarch64",
    define_values = {
        "build_with_mkl_aarch64": "true",
    },
    visibility = ["//visibility:public"],
)

config_setting(
    name = "enable_mkl",
    define_values = {
        "enable_mkl": "true",
        "build_with_mkl": "true",
    },
    visibility = ["//visibility:public"],
)

filegroup(
    name = "LICENSE",
    srcs = ["MKL_LICENSE"] + select({
        "@org_tensorflow//tensorflow:linux_x86_64": [
            "@mkl_linux//:LICENSE",
        ],
        "@org_tensorflow//tensorflow:macos": [
            "@mkl_darwin//:LICENSE",
        ],
        "@org_tensorflow//tensorflow:windows": [
            "@mkl_windows//:LICENSE",
        ],
        "//conditions:default": [],
    }),
    visibility = ["//visibility:public"],
)

cc_library(
    name = "intel_binary_blob",
    visibility = ["//visibility:public"],
    deps = select({
        "@org_tensorflow//tensorflow:linux_x86_64": [
            "@mkl_linux//:mkl_headers",
            "@mkl_linux//:mkl_libs_linux",
        ],
        "@org_tensorflow//tensorflow:macos": [
            "@mkl_darwin//:mkl_headers",
            "@mkl_darwin//:mkl_libs_darwin",
        ],
        "@org_tensorflow//tensorflow:windows": [
            "@mkl_windows//:mkl_headers",
            "@mkl_windows//:mkl_libs_windows",
        ],
        "//conditions:default": [],
    }),
)

bzl_library(
    name = "build_defs_bzl",
    srcs = ["build_defs.bzl"],
    visibility = ["//visibility:public"],
)
