cmake_minimum_required(VERSION 3.0 FATAL_ERROR)

project(memtier_benchmark VERSION 0.4)

set(CMAKE_BUILD_TYPE "DEBUG")
set(CMAKE_C_STANDARD 99)


message(STATUS "Host is: ${CMAKE_HOST_SYSTEM}. Build target is: ${CMAKE_SYSTEM}")
get_filename_component(SRC_ROOT "${CMAKE_CURRENT_SOURCE_DIR}" ABSOLUTE)
message(STATUS "Project root directory is: ${SRC_ROOT}")

#aux_source_directory(src SRC_PROXY)

set(SRC_MEMTIER
        client.cpp, cluster_client.cpp, config_types.cpp, file_io.cpp,
        item.cpp, JSON_handler.cpp, memtier_benchmark.cpp, obj_gen.cpp,
        protocol.cpp, run_stats.cpp, run_stats_types.cpp, shard_connection.cpp
        )

add_executable(memtier_benchmark ${SRC_MEMTIER})
set_target_properties(memtier_benchmark PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${SRC_ROOT}")

target_include_directories(memtier_benchmark
        PRIVATE ${SRC_ROOT}
        )

target_link_libraries(memtier_benchmark
        PRIVATE pthread
        PRIVATE m
        )

