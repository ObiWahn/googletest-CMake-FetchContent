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
target_include_directories(testapp SYSTEM PRIVATE ${gtest_SOURCE_DIR}/include)
target_link_libraries(testapp
    gtest_main gtest
)

