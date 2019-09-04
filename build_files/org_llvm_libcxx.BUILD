package(default_visibility = ["//visibility:public"])

# headers need to be a seperate target as `@org_llvm_libcxxabi//:libcxxabi`
# depends on the headers but `:libcxx` depends on
# `@org_llvm_libcxxabi//:libcxxabi`. This avoids the cycle
cc_library(
    name = "headers",
    hdrs = glob(["include/**"]),
)

cc_library(
    name = "libcxx",
    hdrs = glob(["include/**"]),
    srcs = glob([
        "src/*.cpp",
        "src/include/*.h",
        "src/experimental/*.cpp",
        "filesystem/*.cpp",
        "filesystem/*.h",
    ]),
    textual_hdrs = glob([
        "src/support/runtime/**",
    ]),
    copts = [
        "-Iexternal/org_llvm_libcxx/src/include",
        "-Iexternal/org_llvm_libcxx/src",

        # these definitions are unconditional in CMakeLists.txt
        "-D_LIBCPP_BUILDING_LIBRARY",
        "-D_LIBCPP_HAS_NO_PRAGMA_SYSTEM_HEADER",

        # This is set when building agianst a fresh
        # in tree static libcxxabi
        "-DLIBCXX_BUILDING_LIBCXXABI",
        "-DLIBCXX_CXX_ABI=libcxxabi",

        # exclude the standard c++ headers
        "-nostdinc++",

        # these flags are set unconditionally
        "-fvisibility-inlines-hidden",
        "-Wall",
        "-Wextra",
        "-W",
        "-Wwrite-strings",
        "-Wno-unused-parameter",
        "-Wno-long-long",
        "-Werror=return-type",
        "-Wextra-semi",

        # these flags are set when using clang
        "-Wno-user-defined-literals",
        "-Wno-covered-switch-default",
        "-Wno-ignored-attributes",

        # the toolchain sets std=c++17 so it should be here too
        "-std=c++17",
    ],
    includes = ["include"],
    deps = [
        ":headers",
        "@org_llvm_libcxxabi//:libcxxabi",
    ],
    linkstatic = True,
)
