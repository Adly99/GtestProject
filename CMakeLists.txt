cmake_minimum_required(VERSION 3.10)

# Project name and version
project(MyProject VERSION 1.0)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Enable testing
enable_testing()

# Include directories (assuming headers are in include/)
include_directories(include)

# Automatically gather all source files from src directory
file(GLOB_RECURSE PROJECT_SOURCES src/*.cpp)

# Automatically gather all test files from test directory
file(GLOB_RECURSE TEST_SOURCES test/*.cpp)

# Fetch GoogleTest (version can be changed as needed)
include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/refs/tags/release-1.12.1.zip
  DOWNLOAD_EXTRACT_TIMESTAMP TRUE
)
FetchContent_MakeAvailable(googletest)

# Add the executable for the tests
add_executable(my_test ${PROJECT_SOURCES} ${TEST_SOURCES})

# Register tests with ctest
include(GoogleTest)
gtest_discover_tests(my_test)

# Link the GoogleTest libraries
target_link_libraries(my_test gtest gtest_main)

# Optionally add test manually if needed
add_test(NAME MyCodeTest COMMAND my_test)
