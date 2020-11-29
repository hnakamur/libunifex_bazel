load("@rules_foreign_cc//tools/build_defs:configure.bzl", "configure_make")
load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external")

configure_make(
    name = "liburing",
    lib_source = "@liburing//:all",
    configure_in_place = True,
    shared_libraries = ["liburing.so"],
)

cmake_external(
    name = "libunifex",
    lib_source = "@libunifex//:all",
    cmake_options = ["-GNinja"],
    cache_entries = {
        "MAKE_CXX_STANDARD:STRING": "20",
        "BUILD_TESTING:BOOL": "off",
        "UNIFEX_BUILD_EXAMPLES:BOOL": "off",
    },
    make_commands = [
        "cmake --build . --config Release",
        "install -d \"$BUILD_TMPDIR/$INSTALL_PREFIX/include\"",
        "cp -L -r $EXT_BUILD_ROOT/external/libunifex/include/unifex \"$BUILD_TMPDIR/$INSTALL_PREFIX/include/\"",
        "cp -L -r include/unifex \"$BUILD_TMPDIR/$INSTALL_PREFIX/include/\"",
        "install -D -t \"$BUILD_TMPDIR/$INSTALL_PREFIX/lib\" source/libunifex.a",
    ],
    deps = [":liburing"],
)

cc_binary(
    name = "io_epoll_test",
    srcs = ["io_epoll_test.cpp"],
    deps = [":libunifex"],
)

cc_binary(
    name = "io_uring_test",
    srcs = ["io_uring_test.cpp"],
    deps = [":libunifex"],
)
