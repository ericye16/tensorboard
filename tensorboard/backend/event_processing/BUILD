# Description:
# Event processing logic for TensorBoard

package(default_visibility = ["//visibility:public"])

licenses(["notice"])  # Apache 2.0

exports_files(["LICENSE"])

py_library(
    name = "io_wrapper",
    srcs = ["io_wrapper.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorboard/compat:tensorflow",
        "//tensorboard/util:tb_logging",
        "@org_pythonhosted_six",
    ],
)

py_test(
    name = "io_wrapper_test",
    size = "small",
    srcs = ["io_wrapper_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":io_wrapper",
        "//tensorboard:expect_tensorflow_installed",
        "@org_pythonhosted_six",
    ],
)

py_library(
    name = "data_provider",
    srcs = ["data_provider.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorboard/data:provider",
        "//tensorboard/util:tb_logging",
        "//tensorboard/util:tensor_util",
        "@org_pythonhosted_six",
    ],
)

py_test(
    name = "data_provider_test",
    srcs = ["data_provider_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":data_provider",
        ":event_multiplexer",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/data:provider",
        "//tensorboard/plugins/image:summary_v2",
        "//tensorboard/plugins/scalar:metadata",
        "//tensorboard/plugins/scalar:summary_v2",
        "//tensorboard/util:tensor_util",
        "//tensorboard:expect_tensorflow_installed",
        "@org_pythonhosted_six",
    ],
)

py_library(
    name = "directory_loader",
    srcs = ["directory_loader.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":directory_watcher",
        ":io_wrapper",
        "//tensorboard/compat:tensorflow",
        "//tensorboard/util:tb_logging",
    ],
)

py_test(
    name = "directory_loader_test",
    size = "small",
    srcs = ["directory_loader_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":directory_loader",
        ":directory_watcher",
        ":event_file_loader",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/util:test_util",
        "@org_pythonhosted_mock",
    ],
)

py_library(
    name = "directory_watcher",
    srcs = ["directory_watcher.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":io_wrapper",
        "//tensorboard/compat:tensorflow",
        "//tensorboard/util:tb_logging",
    ],
)

py_test(
    name = "directory_watcher_test",
    size = "small",
    srcs = ["directory_watcher_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":directory_watcher",
        "//tensorboard:expect_tensorflow_installed",
    ],
)

py_library(
    name = "reservoir",
    srcs = ["reservoir.py"],
    srcs_version = "PY2AND3",
)

py_test(
    name = "reservoir_test",
    size = "small",
    srcs = ["reservoir_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":reservoir",
        "//tensorboard:expect_tensorflow_installed",
    ],
)

py_library(
    name = "event_file_loader",
    srcs = ["event_file_loader.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorboard/compat:tensorflow",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/util:platform_util",
        "//tensorboard/util:tb_logging",
    ],
)

py_test(
    name = "event_file_loader_test",
    size = "small",
    srcs = ["event_file_loader_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":event_file_loader",
        "//tensorboard:expect_tensorflow_installed",
    ],
)

py_library(
    name = "event_accumulator",
    srcs = [
        "event_accumulator.py",
        "plugin_event_accumulator.py",
    ],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":directory_loader",
        ":directory_watcher",
        ":event_file_loader",
        ":io_wrapper",
        ":plugin_asset_util",
        ":reservoir",
        "//tensorboard:data_compat",
        "//tensorboard/compat:tensorflow",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/plugins/distribution:compressor",
        "//tensorboard/util:tb_logging",
    ],
)

py_test(
    name = "event_accumulator_test",
    size = "small",
    srcs = ["event_accumulator_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":event_accumulator",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/plugins/audio:summary",
        "//tensorboard/plugins/distribution:compressor",
        "//tensorboard/plugins/image:summary",
        "//tensorboard/plugins/scalar:summary",
        "//tensorboard/util:tensor_util",
        "//tensorboard/util:test_util",
    ],
)

py_test(
    name = "plugin_event_accumulator_test",
    size = "small",
    srcs = ["plugin_event_accumulator_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":event_accumulator",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/plugins/audio:summary",
        "//tensorboard/plugins/distribution:compressor",
        "//tensorboard/plugins/image:summary",
        "//tensorboard/plugins/scalar:summary",
        "//tensorboard/util:tb_logging",
        "//tensorboard/util:tensor_util",
        "//tensorboard/util:test_util",
        "@org_pythonhosted_six",
    ],
)

py_library(
    name = "event_multiplexer",
    srcs = [
        "event_multiplexer.py",
        "plugin_event_multiplexer.py",
    ],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":directory_watcher",
        ":event_accumulator",
        ":io_wrapper",
        "//tensorboard/util:tb_logging",
        "@org_pythonhosted_six",
    ],
)

py_test(
    name = "event_multiplexer_test",
    size = "small",
    srcs = ["event_multiplexer_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":event_accumulator",
        ":event_multiplexer",
        "//tensorboard:expect_tensorflow_installed",
    ],
)

py_test(
    name = "plugin_event_multiplexer_test",
    size = "small",
    srcs = ["plugin_event_multiplexer_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":event_accumulator",
        ":event_multiplexer",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/util:test_util",
    ],
)

py_library(
    name = "db_import_multiplexer",
    srcs = [
        "db_import_multiplexer.py",
    ],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        ":directory_watcher",
        ":event_file_loader",
        ":event_multiplexer",
        ":io_wrapper",
        ":sqlite_writer",
        "//tensorboard:data_compat",
        "//tensorboard/compat:tensorflow",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/util:tb_logging",
        "@org_pythonhosted_six",
    ],
)

py_test(
    name = "db_import_multiplexer_test",
    size = "small",
    srcs = ["db_import_multiplexer_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":db_import_multiplexer",
        "//tensorboard:expect_sqlite3_installed",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/util:tensor_util",
        "//tensorboard/util:test_util",
    ],
)

py_library(
    name = "sqlite_writer",
    srcs = [
        "sqlite_writer.py",
    ],
    srcs_version = "PY2AND3",
    visibility = ["//visibility:public"],
    deps = [
        "//tensorboard/compat:tensorflow",
        "//tensorboard/util:tb_logging",
        "//tensorboard/util:tensor_util",
        "@org_pythonhosted_six",
    ],
)

py_library(
    name = "plugin_asset_util",
    srcs = ["plugin_asset_util.py"],
    srcs_version = "PY2AND3",
    deps = [
        "//tensorboard/compat:tensorflow",
    ],
)

py_library(
    name = "event_file_inspector",
    srcs = ["event_file_inspector.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":event_accumulator",
        ":io_wrapper",
        "//tensorboard/compat:tensorflow",
        "//tensorboard/compat/proto:protos_all_py_pb2",
    ],
)

py_test(
    name = "event_file_inspector_test",
    size = "small",
    srcs = ["event_file_inspector_test.py"],
    srcs_version = "PY2AND3",
    deps = [
        ":event_file_inspector",
        "//tensorboard:expect_tensorflow_installed",
        "//tensorboard/compat/proto:protos_all_py_pb2",
        "//tensorboard/util:test_util",
    ],
)
