workspace(name = "libunifex_bazel")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_foreign_cc",
    strip_prefix = "rules_foreign_cc-master",
    url = "https://github.com/bazelbuild/rules_foreign_cc/archive/master.tar.gz",
)

load("@rules_foreign_cc//:workspace_definitions.bzl", "rules_foreign_cc_dependencies")

rules_foreign_cc_dependencies()

all_content = """filegroup(name = "all", srcs = glob(["**"]), visibility = ["//visibility:public"])"""

http_archive(
    name = "liburing",
    build_file_content = all_content,
    strip_prefix = "liburing-master",
    urls = ["https://github.com/axboe/liburing/archive/master.tar.gz"],
)

http_archive(
    name = "libunifex",
    build_file_content = all_content,
    strip_prefix = "libunifex-master",
    urls = ["https://github.com/facebookexperimental/libunifex/archive/master.tar.gz"],
)
