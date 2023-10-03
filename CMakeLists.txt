# Copyright - Jan Christoph Uhde <Jan@UhdeJC.com>
cmake_minimum_required(VERSION 3.25)
project(googletest-FetchContent VERSION 0.0.1 LANGUAGES CXX)

include(FetchContent)
FetchContent_Declare(
    GTest
    GIT_REPOSITORY https://github.com/google/googletest.git
    GIT_TAG        v1.14.0
    GIT_PROGRESS   TRUE
)

FetchContent_MakeAvailable(GTest)

add_executable(testapp testapp.cpp)
set(BUILD_GMOCK OFF CACHE BOOL "" FORCE)
set(INSTALL_GTEST OFF CACHE BOOL "" FORCE)
message(STATUS "############################################")
message(STATUS "${gtest_SOURCE_DIR}")
set(got_dir "${gtest_SOURCE_DIR}/googletest/include")
set(got_file "${got_dir}/gtest/gtest.h")
if (EXISTS ${got_file})
    message(WARNING "${got_file} exists")
else()
    message(WARNING "${got_file} doe NOT exists")
endif()
message(STATUS "############################################")
include_directories(${got_dir})
target_include_directories(testapp SYSTEM PRIVATE ${gtest_SOURCE_DIR}/googletest/include ${gtest_SOURCE_DIR}/googlemock/include)
target_link_libraries(testapp
    GTest::gtest_main GTest::gtest
)

