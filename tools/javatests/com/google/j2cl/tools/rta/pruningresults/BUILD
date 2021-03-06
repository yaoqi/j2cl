# Description:
#   This package intends to test the pruning result output of the rta algorithm.

package(
    licenses = ["notice"],  # Apache 2.0
)

load("//build_defs:rules.bzl", "j2cl_library", "j2cl_rta")

j2cl_library(
    name = "test_input",
    testonly = 1,
    srcs = [
        "Bar.java",
        "Foo.java",
        "UnusedType.java",
    ],
    deps = ["//third_party:gwt-jsinterop-annotations-j2cl"],
)

j2cl_rta(
    name = "test_input_rta",
    testonly = 1,
    targets = [":test_input"],
)

java_library(
    name = "pruning_results_test_lib",
    testonly = 1,
    srcs = ["PruningResultsTest.java"],
    deps = [
        "//third_party:guava",
        "//third_party:junit",
        "//third_party:truth",
        "//tools/java/com/google/j2cl/tools/minifier",
    ],
)

java_test(
    name = "pruning_results",
    data = [
        ":test_input.js.zip",
        ":test_input_rta_removal_code_info",
    ],
    jvm_flags = [
        "-Dj2cl_rta_removal_code_info_file=$(location :test_input_rta_removal_code_info)",
        "-Dj2cl_zip_file=$(location :test_input.js.zip)",
    ],
    test_class = "com.google.j2cl.tools.rta.pruningresults.PruningResultsTest",
    runtime_deps = [
        ":pruning_results_test_lib",
    ],
)
