# GtestProject

A basic C++ project using Google Test for unit testing. The project demonstrates how to write and run tests for C++ code with a simple and clean directory structure. 

## Project Structure

/GtestProject
  ├── CMakeLists.txt       # Project build configuration file
  ├── src                  # Source files for your application
  │   └── my_code.cpp
  ├── include              # Header files
  │   └── my_code.h
  ├── test                 # Unit test files using Google Test
  │   └── test_my_code.cpp
  └── build/               # Directory where CMake will generate build files
  
## Features

- **Example test cases** using Google Test
- **Modular structure** to easily extend with more code and tests
- **Instructions** for configuring, building, and running tests

## Getting Started

### Prerequisites

Ensure you have the following installed on your system:

- **C++ compiler** (e.g., g++, clang++)
- **CMake** (build system generator)
- **Google Test** (included via CMake, or you can link it externally)

### Installation

Follow these steps to clone, build, and run the project:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/gtestproject.git
   cd GtestProject
2.**Configure and build the project**: Run the following commands to clean the build directory, configure the project using CMake, and build it:

***rm -rf build/* && cmake -S . -B build && cmake --build build -j***
- rm -rf build/: Clears the build directory to ensure a clean build.
- cmake -S . -B build: Configures the project from the source (.) and generates build files in the build/ directory.
- cmake --build build -j: Builds the project using all available CPU cores for faster compilation.

3.**Debugging Errors (Optional)**: If there are any build errors, redirect them to an error log file for troubleshooting:
-> cmake --build build -j 2> ./build/error.log

