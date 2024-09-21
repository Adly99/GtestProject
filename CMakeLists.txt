cmake_minimum_required(VERSION 3.28.3)

# Project name and version
project(GtestProject VERSION 1.0 LANGUAGES CXX)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)
set(CMAKE_CXX_EXTENSIONS FALSE)  # Avoid compiler-specific extensions

message(STATUS "Configuring GtestProject version ${PROJECT_VERSION} with C++17.")

# Enable testing
enable_testing()

# Include directories (assuming headers are in include/)
include_directories(include)

# Automatically gather all source files from src directory
file(GLOB_RECURSE PROJECT_SOURCES src/*.cpp)
message(STATUS "Found source files: ${PROJECT_SOURCES}")

# Automatically gather all test files from test directory
file(GLOB_RECURSE TEST_SOURCES test/*.cpp)
message(STATUS "Found test files: ${TEST_SOURCES}")

# Include FetchContent module to download and configure dependencies
include(FetchContent)

# Fetch GoogleTest with the latest stable release (v1.15.2)
message(STATUS "Fetching GoogleTest...")
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/refs/tags/v1.15.2.zip  # Latest stable release (v1.15.2)
  DOWNLOAD_EXTRACT_TIMESTAMP TRUE  # Ensure reproducible builds
)

# Make GoogleTest available for the project
FetchContent_MakeAvailable(googletest)
message(STATUS "GoogleTest successfully fetched and made available.")

# Add the executable for the tests
add_executable(my_test ${PROJECT_SOURCES} ${TEST_SOURCES})
message(STATUS "Creating executable for tests: my_test")

# Link the GoogleTest libraries
target_link_libraries(my_test gtest gtest_main)
message(STATUS "Linked GoogleTest libraries to my_test.")

# Register tests with ctest
include(GoogleTest)
gtest_discover_tests(my_test)
message(STATUS "Registered tests with CTest.")

# Optionally add test manually if needed
add_test(NAME MyCodeTest COMMAND my_test)

# Set output directories for built binaries
set_target_properties(my_test PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
)
message(STATUS "Set output directories for built binaries.")

