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
* Modified code (TutorialConfig.h)
  ```h
  // the configured options and settings for Tutorial
  #define Tutorial_VERSION_MAJOR @Tutorial_VERSION_MAJOR@
  #define Tutorial_VERSION_MINOR @Tutorial_VERSION_MINOR@
  #cmakedefine USE_MYMATH
  ```
* `tutorial.cxx`
  ```c++
  // A simple program that computes the square root of a number
  #include <cmath>
  #include <iostream>
  #include <string>

  #include "TutorialConfig.h"

  #ifdef USE_MYMATH
  #  include "MathFunctions/MathFunctions.h"
  #endif

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
    #ifdef USE_MYMATH
      const double outputValue = mysqrt(inputValue);
    #else
      const double outputValue = sqrt(inputValue);
    #endif
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

  option(USE_MYMATH "Use tutorial provided math implementation" ON)


  # configure a header file to pass some of the CMake settings
  # to the source code
  configure_file(TutorialConfig.h.in TutorialConfig.h)

  # add the MathFunctions library
  #add_subdirectory(MathFunctions)

  if(USE_MYMATH)
    add_subdirectory(MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
    list(APPEND EXTRA_INCLUDES "${PROJECT_SOURCE_DIR}/MathFunctions")
  endif()

  # add the executable
  add_executable(Tutorial tutorial.cxx)

  target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

  # add the binary tree to the search path for include files
  # so that we will find TutorialConfig.h
  target_include_directories(Tutorial PUBLIC
                             "${PROJECT_BINARY_DIR}"
                             )
  ```
* Running Tutorial again
  ![part2](https://user-images.githubusercontent.com/49171429/174686839-96bc3be4-87a6-407c-8c39-bedca60d5750.png)

### Step 3
* `CMakeLists.txt`
  ```
  cmake_minimum_required(VERSION 3.10)

  # set the project name and version
  project(Tutorial VERSION 1.0)

  # specify the C++ standard
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED True)

  # should we use our own math functions
  option(USE_MYMATH "Use tutorial provided math implementation" ON)

  # configure a header file to pass some of the CMake settings
  # to the source code
  configure_file(TutorialConfig.h.in TutorialConfig.h)

  # add the MathFunctions library
  if(USE_MYMATH)
    add_subdirectory(MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
  endif()

  # add the executable
  add_executable(Tutorial tutorial.cxx)

  target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

  # add the binary tree to the search path for include files
  # so that we will find TutorialConfig.h
  target_include_directories(Tutorial PUBLIC
                             "${PROJECT_BINARY_DIR}"
                             )
  ```
* `MathFunctions/CMakeLists.txt`
  ```
  add_library(MathFunctions mysqrt.cxx)
  target_include_directories(MathFunctions
            INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
            )
  ```
* Tutorial Screenshot
  ![part3](https://user-images.githubusercontent.com/49171429/174689434-d2a1eb48-9c47-4d2d-8817-bf7ddc2cd834.png)

### Step 4
* `CMakeLists.txt`
  ```
  cmake_minimum_required(VERSION 3.10)

  # set the project name and version
  project(Tutorial VERSION 1.0)

  # specify the C++ standard
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED True)

  # should we use our own math functions
  option(USE_MYMATH "Use tutorial provided math implementation" ON)

  # configure a header file to pass some of the CMake settings
  # to the source code
  configure_file(TutorialConfig.h.in TutorialConfig.h)

  # add the MathFunctions library
  if(USE_MYMATH)
    add_subdirectory(MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
  endif()

  # add the executable
  add_executable(Tutorial tutorial.cxx)

  target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

  # add the binary tree to the search path for include files
  # so that we will find TutorialConfig.h
  target_include_directories(Tutorial PUBLIC
                             "${PROJECT_BINARY_DIR}"
                             )

  install(TARGETS Tutorial DESTINATION bin)
  install(FILES "${PROJECT_BINARY_DIR}/TutorialConfig.h"
    DESTINATION include
    )

  # TESTING
  enable_testing()

  # does the application run
  add_test(NAME Runs COMMAND Tutorial 25)

  # does the usage message work?
  add_test(NAME Usage COMMAND Tutorial)
  set_tests_properties(Usage
    PROPERTIES PASS_REGULAR_EXPRESSION "Usage:.*number"
    )

  # define a function to simplify adding tests
  function(do_test target arg result)
    add_test(NAME Comp${arg} COMMAND ${target} ${arg})
    set_tests_properties(Comp${arg}
      PROPERTIES PASS_REGULAR_EXPRESSION ${result}
      )
  endfunction()

  # do a bunch of result based tests
  do_test(Tutorial 4 "4 is 2")
  do_test(Tutorial 9 "9 is 3")
  do_test(Tutorial 5 "5 is 2.236")
  do_test(Tutorial 7 "7 is 2.645")
  do_test(Tutorial 25 "25 is 5")
  do_test(Tutorial -25 "-25 is (-nan|nan|0)")
  do_test(Tutorial 0.0001 "0.0001 is 0.01")
  ```
* `MathFunctions/CMakeLists.txt`
  ```
  add_library(MathFunctions mysqrt.cxx)

  # state that anybody linking to us needs to include the current source dir
  # to find MathFunctions.h, while we don't.
  target_include_directories(MathFunctions
            INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
            )

  install(TARGETS MathFunctions DESTINATION lib)
  install(FILES MathFunctions.h DESTINATION include)
  ```
* Running ctest -VV
  ![step4](https://user-images.githubusercontent.com/49171429/174690629-b1afecbe-03d4-4a4c-b03d-de23b65a9944.png)

### Step 5
* `CMakeLists.txt`
  ```
  cmake_minimum_required(VERSION 3.10)

  # set the project name and version
  project(Tutorial VERSION 1.0)

  # specify the C++ standard
  set(CMAKE_CXX_STANDARD 11)
  set(CMAKE_CXX_STANDARD_REQUIRED True)

  # should we use our own math functions
  option(USE_MYMATH "Use tutorial provided math implementation" ON)

  # configure a header file to pass some of the CMake settings
  # to the source code
  configure_file(TutorialConfig.h.in TutorialConfig.h)

  # add the MathFunctions library
  if(USE_MYMATH)
    add_subdirectory(MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
  endif()

  # add the executable
  add_executable(Tutorial tutorial.cxx)
  target_link_libraries(Tutorial PUBLIC ${EXTRA_LIBS})

  # add the binary tree to the search path for include files
  # so that we will find TutorialConfig.h
  target_include_directories(Tutorial PUBLIC
                             "${PROJECT_BINARY_DIR}"
                             )

  # add the install targets
  install(TARGETS Tutorial DESTINATION bin)
  install(FILES "${PROJECT_BINARY_DIR}/TutorialConfig.h"
    DESTINATION include
    )

  # enable testing
  enable_testing()

  # does the application run
  add_test(NAME Runs COMMAND Tutorial 25)

  # does the usage message work?
  add_test(NAME Usage COMMAND Tutorial)
  set_tests_properties(Usage
    PROPERTIES PASS_REGULAR_EXPRESSION "Usage:.*number"
    )

  # define a function to simplify adding tests
  function(do_test target arg result)
    add_test(NAME Comp${arg} COMMAND ${target} ${arg})
    set_tests_properties(Comp${arg}
      PROPERTIES PASS_REGULAR_EXPRESSION ${result}
      )
  endfunction()

  # do a bunch of result based tests
  do_test(Tutorial 4 "4 is 2")
  do_test(Tutorial 9 "9 is 3")
  do_test(Tutorial 5 "5 is 2.236")
  do_test(Tutorial 7 "7 is 2.645")
  do_test(Tutorial 25 "25 is 5")
  do_test(Tutorial -25 "-25 is (-nan|nan|0)")
  do_test(Tutorial 0.0001 "0.0001 is 0.01")
  ```
* `MathFunctions/CMakeLists.txt`
  ```
  add_library(MathFunctions mysqrt.cxx)

  # state that anybody linking to us needs to include the current source dir
  # to find MathFunctions.h, while we don't.
  target_include_directories(MathFunctions
            INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}
            )
  # does this system provide the log and exp functions?
  include(CheckCXXSourceCompiles)
  check_cxx_source_compiles("
    #include <cmath>
    int main() {
      std::log(1.0);
      return 0;
    }
  " HAVE_LOG)
  check_cxx_source_compiles("
    #include <cmath>
    int main() {
      std::exp(1.0);
      return 0;
    }
  " HAVE_EXP)

  if(HAVE_LOG AND HAVE_EXP)
    target_compile_definitions(MathFunctions
                               PRIVATE "HAVE_LOG" "HAVE_EXP")
  endif()

  # install rules
  install(TARGETS MathFunctions DESTINATION lib)
  install(FILES MathFunctions.h DESTINATION include)
  ```
* Tutorial with USE_MYMATH
  ![part5](https://user-images.githubusercontent.com/49171429/174692033-8061bf2e-cb7e-4d88-bbc8-5cd5783317d7.png)

## Part Two: Custom build
* `MakeFile`
* `CMakeLists.txt`
* `CMake generated MakeFile`
* Difference in sizes
* Output
