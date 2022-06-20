# Lab 5

## Part One: [Cmake Tutorial](https://cmake.org/cmake/help/latest/guide/tutorial/index.html) 
### Step 1
* Modified code (TutorialConfig.h)
  ```h
  // the configured options and settings for Tutorial
  #define Tutorial_VERSION_MAJOR @Tutorial_VERSION_MAJOR@
  #define Tutorial_VERSION_MINOR @Tutorial_VERSION_MINOR@
  ```
* `tutorial.cxx`
  ```c++
    // A simple program that computes the square root of a number
  #include <cmath>
  #include <iostream>
  #include <string>
  #include "TutorialConfig.h"

  int main(int argc, char* argv[])
  {
    if (argc < 2) {
      // report version
      std::cout << argv[0] << " Version " << Tutorial_VERSION_MAJOR << "."
                << Tutorial_VERSION_MINOR << std::endl;
      std::cout << "Usage: " << argv[0] << " number" << std::endl;
      return 1;
    }

    // convert input to double
    const double inputValue = std::stod(argv[1]);

    // calculate square root
    const double outputValue = sqrt(inputValue);
    std::cout << "The square root of " << inputValue << " is " << outputValue
              << std::endl;
    return 0;
  }
  ```
* `CMakeLists.txt`
  ```
  cmake_minimum_required(VERSION 3.10)

  # set the project name and version
  project(Tutorial VERSION 1.0)

  # specify the C++ standard
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED True)

  configure_file(TutorialConfig.h.in TutorialConfig.h)

  # add the executable
  add_executable(Tutorial tutorial.cxx)

  target_include_directories(Tutorial PUBLIC
                               "${PROJECT_BINARY_DIR}"
                                        )
  ```
* Running Tutorial
  ![part1](https://user-images.githubusercontent.com/49171429/174684505-7ef6fc83-24d3-4d4b-b68c-77b9dcebddbb.png)

### Step 2
### Step 3
### Step 4
### Step 5
