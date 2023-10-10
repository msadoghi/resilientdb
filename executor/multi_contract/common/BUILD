package(default_visibility = ["//visibility:public"])

cc_library(
    name = "utils",
    hdrs = ["utils.h"],
    deps = [
        "//third_party:evm_lib",
    ],
)

cc_library(
    name = "contract_verifier",
    hdrs = ["contract_verifier.h"],
    srcs = ["contract_verifier.cpp"],
    deps = [
        ":contract_executor",
        ":contract_committer",
        ":committer_context",
        "//service/contract/proto:func_params_cc_proto",
    ],
)

cc_library(
    name = "x_verifier",
    srcs = ["x_verifier.cpp"],
    hdrs = ["x_verifier.h"],
    deps = [
        ":contract_verifier",
        ":local_state",
        ":global_state",
        ":v_controller",
        "//common/utils:utils",
        "//platform/common/queue:lock_free_queue",
        "//service/contract/proto:func_params_cc_proto",
    ],
)

cc_test(
    name = "x_committer_test",
    srcs = ["x_committer_test.cpp"],
    data = [
        "//service/contract/executor/manager/test_data:contract.json",
    ],
    deps = [
        ":contract_deployer",
        ":x_committer",
        ":address_manager",
        ":mock_data_storage",
        "//common/test:test_main",
    ],
)

cc_test(
    name = "x_verifier_test",
    srcs = ["x_verifier_test.cpp"],
    data = [
        "//service/contract/executor/manager/test_data:contract.json",
        "//service/contract/executor/manager/test_data:kv.json",
    ],
    deps = [
        ":contract_deployer",
        ":x_verifier",
        ":x_committer",
        ":address_manager",
        ":mock_data_storage",
        "//common/test:test_main",
    ],
)

cc_library(
    name = "streaming_single_committer",
    srcs = ["streaming_single_committer.cpp"],
    hdrs = ["streaming_single_committer.h"],
    deps = [
        ":committer_context",
        ":contract_committer",
        ":contract_executor",
        ":global_state",
        "//common/utils:utils",
        "//service/contract/proto:func_params_cc_proto",
    ],
)

cc_library(
    name = "streaming_dq_committer",
    srcs = ["streaming_dq_committer.cpp"],
    hdrs = ["streaming_dq_committer.h"],
    deps = [
        ":committer_context",
        ":contract_committer",
        ":contract_executor",
        ":streaming_dq_controller",
        ":local_state",
        ":global_state",
        "//common/utils:utils",
        "//platform/common/queue:lock_free_queue",
        "//service/contract/proto:func_params_cc_proto",
    ],
)

cc_test(
    name = "streaming_dq_committer_test",
    srcs = ["streaming_dq_committer_test.cpp"],
    data = [
        "//service/contract/executor/manager/test_data:contract.json",
        "//service/contract/executor/manager/test_data:kv.json",
    ],
    deps = [
        ":contract_deployer",
        ":address_manager",
        ":mock_d_storage",
        ":streaming_dq_committer",
        "//common/test:test_main",
    ],
)


cc_test(
    name = "sequential_concurrency_committer_test",
    srcs = ["sequential_concurrency_committer_test.cpp"],
    data = [
        "//service/contract/executor/manager/test_data:contract.json",
    ],
    deps = [
        ":contract_deployer",
        ":address_manager",
        ":mock_data_storage",
        ":sequential_concurrency_committer",
        "//common/test:test_main",
    ],
)

cc_library(
    name = "streaming_controller",
    srcs = ["streaming_controller.cpp"],
    hdrs = ["streaming_controller.h"],
    deps = [
        ":concurrency_controller",
        "//platform/common/queue:lock_free_queue",
        "//common:comm",
    ],
)

cc_library(
    name = "streaming_committer",
    srcs = ["streaming_committer.cpp"],
    hdrs = ["streaming_committer.h"],
    deps = [
        ":contract_committer",
        ":contract_executor",
        ":streaming_controller",
        ":local_state",
        ":global_state",
        "//common/utils:utils",
        "//platform/common/queue:lock_free_queue",
        "//service/contract/proto:func_params_cc_proto",
    ],
)

cc_library(
    name = "test_committer",
    hdrs = ["test_committer.h"],
    srcs = ["test_committer.cpp"],
    testonly = True,
    deps = [
        ":test_controller",
        ":contract_committer",
        ":contract_executor",
        ":global_state",
        "//service/contract/proto:func_params_cc_proto",
    ],
)

cc_library(
    name = "contract_deployer",
    srcs = ["contract_deployer.cpp"],
    hdrs = ["contract_deployer.h"],
    deps = [
        ":concurrency_controller",
        ":contract_committer",
        ":global_state",
        ":address_manager",
    ],
)

cc_test(
    name = "contract_deployer_test",
    srcs = ["contract_deployer_test.cpp"],
    data = [
        "//service/contract/executor/manager/test_data:contract.json",
    ],
    deps = [
        ":test_committer",
        ":contract_deployer",
        "//common/test:test_main",
    ],
)

cc_library(
    name = "contract_manager",
    srcs = ["contract_manager.cpp"],
    hdrs = ["contract_manager.h"],
    deps = [
        ":contract_deployer",
        ":two_phase_committer",
        ":sequential_concurrency_committer",
        ":ooo_committer",
        ":two_phase_ooo_committer",
        ":x_committer",
        ":x_verifier",
        ":streaming_committer",
        ":concurrency_controller",
        ":streaming_single_committer",
        ":streaming_dq_committer",
        ":global_state",
        ":address_manager",
        ":utils",
        "//common:comm",
        "//service/contract/proto:func_params_cc_proto",
    ],
)

cc_test(
    name = "contract_manager_test",
    srcs = ["contract_manager_test.cpp"],
    data = [
        "//service/contract/executor/manager/test_data:contract.json",
    ],
    deps = [
        ":contract_manager",
        "//common/test:test_main",
    ],
)

