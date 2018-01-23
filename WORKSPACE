workspace(name = "proto_udsupsver_colabsaumoh")

git_repository(
    name = "io_bazel_rules_go",
    remote = "https://github.com/bazelbuild/rules_go.git",
    commit = "3930b2cdd78a896cae3c6d25b6e3e3b7ea7b8128"
)

load("@io_bazel_rules_go//go:def.bzl", "go_rules_dependencies", "go_register_toolchains")
go_rules_dependencies()
go_register_toolchains()

git_repository(
	name = "org_pubref_rules_protobuf",
	remote = "https://github.com/pubref/rules_protobuf.git",
	commit = "563b674a2ce6650d459732932ea2bc98c9c9a9bf"
)
load("@org_pubref_rules_protobuf//protobuf:rules.bzl", "proto_repositories")

proto_repositories()

load("@org_pubref_rules_protobuf//go:rules.bzl", "go_proto_repositories")

go_proto_repositories()

load("@io_bazel_rules_go//go:def.bzl", "go_repository")

go_repository(
    name = "com_github_spf13_pflag",
    commit = "e57e3eeb33f795204c1ca35f56c44f83227c6e66",
    importpath = "github.com/spf13/pflag",
)

go_repository(
    name = "com_github_spf13_cobra",
    commit = "2df9a531813370438a4d79bfc33e21f58063ed87",
    importpath = "github.com/spf13/cobra",
)

#
# Needed for gatering the pb.go's dependency on gRPC status.pb.go
#
go_repository(
    name = "org_golang_google_genproto",
    importpath = "github.com/google/go-genproto",
)

## Needed for including google/grpc/status.proto in a protobuf definition
GOOGLEAPIS_SHA="5c6df0cd18c6a429eab739fb711c27f6e1393366" # May 14, 2017
new_http_archive(
   name = "googleapi",
   strip_prefix = "googleapis-" + GOOGLEAPIS_SHA,
   urls = [
      "https://github.com/googleapis/googleapis/archive/" + GOOGLEAPIS_SHA + ".tar.gz",
   ],
   build_file_content = """
load("@com_google_protobuf//:protobuf.bzl", "cc_proto_library")

filegroup(
    name = "rpc_status_protos_src",
    srcs = [
        "google/rpc/status.proto",
    ],
    visibility = ["//visibility:public"],
 )
"""
)
