load("//tensorstore:tensorstore.bzl", "tensorstore_cc_library", "tensorstore_cc_test")

package(default_visibility = ["//visibility:public"])

licenses(["notice"])

tensorstore_cc_library(
    name = "chunk",
    hdrs = ["chunk.h"],
    deps = [
        "//tensorstore:data_type",
        "//tensorstore/index_space:index_transform",
        "//tensorstore/internal:arena",
        "//tensorstore/internal:element_copy_function",
        "//tensorstore/internal:elementwise_function",
        "//tensorstore/internal:nditerable",
        "//tensorstore/internal:poly",
        "//tensorstore/util:future",
        "//tensorstore/util:sender",
        "//tensorstore/util:status",
    ],
)

tensorstore_cc_library(
    name = "driver",
    srcs = ["driver.cc"],
    hdrs = [
        "driver.h",
        "registry.h",
    ],
    deps = [
        ":chunk",
        "//tensorstore:context",
        "//tensorstore:open_mode",
        "//tensorstore:progress",
        "//tensorstore:resize_options",
        "//tensorstore:spec_request_options",
        "//tensorstore/index_space:alignment",
        "//tensorstore/index_space:index_transform",
        "//tensorstore/index_space:index_transform_spec",
        "//tensorstore/index_space:json",
        "//tensorstore/index_space:transformed_array",
        "//tensorstore/internal:arena",
        "//tensorstore/internal:context_binding",
        "//tensorstore/internal:data_type_json_binder",
        "//tensorstore/internal:intrusive_ptr",
        "//tensorstore/internal:json",
        "//tensorstore/internal:json_registry",
        "//tensorstore/internal:nditerable_copy",
        "//tensorstore/internal:nditerable_data_type_conversion",
        "//tensorstore/internal:nditerable_transformed_array",
        "//tensorstore/internal:no_destructor",
        "//tensorstore/util:executor",
        "//tensorstore/util:future",
        "//tensorstore/util:quote_string",
        "//tensorstore/util:sender",
        "//tensorstore/util:status",
        "@com_google_absl//absl/strings",
    ],
)

tensorstore_cc_test(
    name = "driver_test",
    size = "small",
    srcs = ["driver_test.cc"],
    deps = [
        ":driver",
        "//tensorstore:array",
        "//tensorstore:context",
        "//tensorstore:index",
        "//tensorstore/index_space:index_transform",
        "//tensorstore/util:executor",
        "//tensorstore/util:status",
        "//tensorstore/util:status_testutil",
        "//tensorstore/util:str_cat",
        "@com_google_googletest//:gtest_main",
    ],
)

tensorstore_cc_library(
    name = "driver_testutil",
    testonly = 1,
    srcs = ["driver_testutil.cc"],
    hdrs = ["driver_testutil.h"],
    deps = [
        "//tensorstore",
        "//tensorstore:array",
        "//tensorstore:data_type",
        "//tensorstore:json_serialization_options",
        "//tensorstore:open",
        "//tensorstore:spec_request_options",
        "//tensorstore/index_space:dim_expression",
        "//tensorstore/index_space:index_transform",
        "//tensorstore/index_space:index_transform_builder",
        "//tensorstore/internal:data_type_random_generator",
        "//tensorstore/internal:logging",
        "//tensorstore/util:status_testutil",
        "@com_github_nlohmann_json//:nlohmann_json",
        "@com_google_absl//absl/algorithm:container",
        "@com_google_googletest//:gtest",
    ],
)

tensorstore_cc_library(
    name = "kvs_backed_chunk_driver",
    srcs = [
        "kvs_backed_chunk_driver.cc",
    ],
    hdrs = [
        "kvs_backed_chunk_driver.h",
        "kvs_backed_chunk_driver_impl.h",
    ],
    deps = [
        ":driver",
        "//tensorstore",
        "//tensorstore:box",
        "//tensorstore:index",
        "//tensorstore:open_mode",
        "//tensorstore:spec",
        "//tensorstore/index_space:index_transform",
        "//tensorstore/internal:aggregate_writeback_cache",
        "//tensorstore/internal:async_storage_backed_cache",
        "//tensorstore/internal:box_difference",
        "//tensorstore/internal:cache_key",
        "//tensorstore/internal:cache_pool_resource",
        "//tensorstore/internal:chunk_cache",
        "//tensorstore/internal:context_binding",
        "//tensorstore/internal:data_copy_concurrency_resource",
        "//tensorstore/internal:intrusive_ptr",
        "//tensorstore/internal:json",
        "//tensorstore/internal:key_value_store_cache",
        "//tensorstore/internal:open_mode_spec",
        "//tensorstore/internal:staleness_bound_json_binder",
        "//tensorstore/internal:type_traits",
        "//tensorstore/kvstore:key_value_store",
        "//tensorstore/util:bit_span",
        "//tensorstore/util:bit_vec",
        "//tensorstore/util:future",
        "//tensorstore/util:iterate_over_index_range",
        "//tensorstore/util:quote_string",
        "//tensorstore/util:result",
        "@com_google_absl//absl/container:fixed_array",
        "@com_google_absl//absl/container:inlined_vector",
        "@com_google_absl//absl/strings",
    ],
)

tensorstore_cc_test(
    name = "kvs_backed_chunk_driver_test",
    size = "small",
    srcs = ["kvs_backed_chunk_driver_test.cc"],
    deps = [
        ":kvs_backed_chunk_driver",
        "//tensorstore:box",
        "//tensorstore:index",
        "//tensorstore/util:span",
        "//tensorstore/util:status",
        "//tensorstore/util:status_testutil",
        "@com_google_googletest//:gtest_main",
    ],
)
