subinclude("//build_defs:go_bindata")

go_bindata(
    name = "static_files",
    srcs = glob(["static/*.*"]),
    prefix = "$PKG/static",
)

go_library(
    name = "rpc",
    srcs = [
        "auth.go",
        "rpc.go",
        ":static_files",
    ],
    visibility = ["//lucidity/..."],
    deps = [
        "//grpcutil",
        "//proto:lucidity",
        "//third_party/go:api",
        "//third_party/go:cli-init",
        "//third_party/go:protobuf",
        "//third_party/go/prometheus",
    ],
)

go_test(
    name = "rpc_test",
    srcs = ["rpc_test.go"],
    deps = [
        ":rpc",
        "//proto:lucidity",
        "//third_party/go:testify",
    ],
)

sh_cmd(
    name = "generate",
    data = [":static_files"],
    cmd = "cp $(out_location :static_files) lucidity/rpc/",
    labels = ["codegen"],
)
