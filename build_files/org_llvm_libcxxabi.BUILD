package(default_visibility = ["//visibility:public"])

cc_library(
    name = "libcxxabi",
    hdrs = glob(["include/**"]),
    srcs = glob([
        "src/*.cpp",
        "src/*.hpp",
        "src/*.h",
        "src/include/*.h",
        "src/demangle/*.h",
    ], exclude = [
        # exclude new/delete definitions from libc++abi. They are
        # provided by libc++. This causes GCC 4.9 to fail to link
        # applications correctly, but we're using clang.
        "src/stdlib_new_delete.cpp",
        # exceptions are enabled, therefore exclude this.
        "src/cxa_noexception.cpp",
    ]),
    copts = [
        "-Iexternal/org_llvm_libcxx/include",

        # The following definitions are set unconditionally
        "-D_LIBCPP_DISABLE_EXTERN_TEMPLATE",
        "-D_LIBCPP_ENABLE_CXX17_REMOVED_UNEXPECTED_FUNCTIONS",
        "-D_LIBCXXABI_BUILDING_LIBRARY",

        # The following flags are set unconditionally
        "-Werror=return-type",
        "-W",
        "-Wall",
        "-Wchar-subscripts",
        "-Wconversion",
        "-Wmismatched-tags",
        "-Wmissing-braces",
        "-Wnewline-eof",
        "-Wunused-function",
        "-Wshadow",
        "-Wshorten-64-to-32",
        "-Wsign-compare",
        "-Wsign-conversion",
        "-Wstrict-aliasing=2",
        "-Wstrict-overflow=4",
        "-Wunused-parameter",
        "-Wunused-variable",
        "-Wwrite-strings",
        "-Wundef",
        "-fstrict-aliasing",

        # Don't include standard c++ headers
        "-nostdinc++",

        # copts when exceptions are enabled
        "-funwind-tables",
    ],
    includes = ["include"],
    deps = ["@org_llvm_libcxx//:headers"],
    linkstatic = True,
)
