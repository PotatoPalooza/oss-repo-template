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
  ```
  all: static shared

  static:
    gcc -c -fPIC -o static_block.o source/block.c
    ar rcs libstaticblock.a static_block.o
    gcc program.c libstaticblock.a -o static_block

  shared:
    gcc -c -fPIC -o dynamic_block.o source/block.c
    gcc -shared -o libdynamic_block.so dynamic_block.o
    gcc -L. program.c -o dynamic_block -ldynamic_block
  ```
* `CMakeLists.txt`
  ```
  cmake_minimum_required(VERSION 3.10)

  project(Program VERSION 1.0)

  add_library(staticlib STATIC source/block.c headers/block.h)
  add_executable(static_block program.c)
  target_link_libraries(static_block PUBLIC staticlib)

  add_library(dynamiclib SHARED source/block.c headers/block.h)
  add_executable(dynamic_block program.c)
  target_link_libraries(dynamic_block PUBLIC dynamiclib)
  ```
* `CMake generated MakeFile`
  ```
  # CMAKE generated file: DO NOT EDIT!
  # Generated by "Unix Makefiles" Generator, CMake Version 3.16

  # Default target executed when no arguments are given to make.
  default_target: all

  .PHONY : default_target

  # Allow only one "make -f Makefile2" at a time, but pass parallelism.
  .NOTPARALLEL:


  #=============================================================================
  # Special targets provided by cmake.

  # Disable implicit rules so canonical targets will work.
  .SUFFIXES:


  # Remove some rules from gmake that .SUFFIXES does not remove.
  SUFFIXES =

  .SUFFIXES: .hpux_make_needs_suffix_list


  # Suppress display of executed commands.
  $(VERBOSE).SILENT:


  # A target that is always out of date.
  cmake_force:

  .PHONY : cmake_force

  #=============================================================================
  # Set environment variables for the build.

  # The shell in which to execute make rules.
  SHELL = /bin/sh

  # The CMake executable.
  CMAKE_COMMAND = /usr/bin/cmake

  # The command to remove a file.
  RM = /usr/bin/cmake -E remove -f

  # Escaping for special characters.
  EQUALS = =

  # The top-level source directory on which CMake was run.
  CMAKE_SOURCE_DIR = /mnt/c/RPI/Junior/Summer/OSS/labs/lab5/CSCI-4470-OpenSource/Modules/05.BuildSystems/Lab-BuildSystemsExample

  # The top-level build directory on which CMake was run.
  CMAKE_BINARY_DIR = /mnt/c/RPI/Junior/Summer/OSS/labs/lab5/CSCI-4470-OpenSource/Modules/05.BuildSystems/Lab-BuildSystemsExample/build

  #=============================================================================
  # Targets provided globally by CMake.

  # Special rule for the target rebuild_cache
  rebuild_cache:
    @$(CMAKE_COMMAND) -E cmake_echo_color --switch=$(COLOR) --cyan "Running CMake to regenerate build system..."
    /usr/bin/cmake -S$(CMAKE_SOURCE_DIR) -B$(CMAKE_BINARY_DIR)
  .PHONY : rebuild_cache

  # Special rule for the target rebuild_cache
  rebuild_cache/fast: rebuild_cache

  .PHONY : rebuild_cache/fast

  # Special rule for the target edit_cache
  edit_cache:
    @$(CMAKE_COMMAND) -E cmake_echo_color --switch=$(COLOR) --cyan "No interactive CMake dialog available..."
    /usr/bin/cmake -E echo No\ interactive\ CMake\ dialog\ available.
  .PHONY : edit_cache

  # Special rule for the target edit_cache
  edit_cache/fast: edit_cache

  .PHONY : edit_cache/fast

  # The main all target
  all: cmake_check_build_system
    $(CMAKE_COMMAND) -E cmake_progress_start /mnt/c/RPI/Junior/Summer/OSS/labs/lab5/CSCI-4470-OpenSource/Modules/05.BuildSystems/Lab-BuildSystemsExample/build/CMakeFiles /mnt/c/RPI/Junior/Summer/OSS/labs/lab5/CSCI-4470-OpenSource/Modules/05.BuildSystems/Lab-BuildSystemsExample/build/CMakeFiles/progress.marks
    $(MAKE) -f CMakeFiles/Makefile2 all
    $(CMAKE_COMMAND) -E cmake_progress_start /mnt/c/RPI/Junior/Summer/OSS/labs/lab5/CSCI-4470-OpenSource/Modules/05.BuildSystems/Lab-BuildSystemsExample/build/CMakeFiles 0
  .PHONY : all

  # The main clean target
  clean:
    $(MAKE) -f CMakeFiles/Makefile2 clean
  .PHONY : clean

  # The main clean target
  clean/fast: clean

  .PHONY : clean/fast

  # Prepare targets for installation.
  preinstall: all
    $(MAKE) -f CMakeFiles/Makefile2 preinstall
  .PHONY : preinstall

  # Prepare targets for installation.
  preinstall/fast:
    $(MAKE) -f CMakeFiles/Makefile2 preinstall
  .PHONY : preinstall/fast

  # clear depends
  depend:
    $(CMAKE_COMMAND) -S$(CMAKE_SOURCE_DIR) -B$(CMAKE_BINARY_DIR) --check-build-system CMakeFiles/Makefile.cmake 1
  .PHONY : depend

  #=============================================================================
  # Target rules for targets named dynamiclib

  # Build rule for target.
  dynamiclib: cmake_check_build_system
    $(MAKE) -f CMakeFiles/Makefile2 dynamiclib
  .PHONY : dynamiclib

  # fast build rule for target.
  dynamiclib/fast:
    $(MAKE) -f CMakeFiles/dynamiclib.dir/build.make CMakeFiles/dynamiclib.dir/build
  .PHONY : dynamiclib/fast

  #=============================================================================
  # Target rules for targets named dynamic_block

  # Build rule for target.
  dynamic_block: cmake_check_build_system
    $(MAKE) -f CMakeFiles/Makefile2 dynamic_block
  .PHONY : dynamic_block

  # fast build rule for target.
  dynamic_block/fast:
    $(MAKE) -f CMakeFiles/dynamic_block.dir/build.make CMakeFiles/dynamic_block.dir/build
  .PHONY : dynamic_block/fast

  #=============================================================================
  # Target rules for targets named static_block

  # Build rule for target.
  static_block: cmake_check_build_system
    $(MAKE) -f CMakeFiles/Makefile2 static_block
  .PHONY : static_block

  # fast build rule for target.
  static_block/fast:
    $(MAKE) -f CMakeFiles/static_block.dir/build.make CMakeFiles/static_block.dir/build
  .PHONY : static_block/fast

  #=============================================================================
  # Target rules for targets named staticlib

  # Build rule for target.
  staticlib: cmake_check_build_system
    $(MAKE) -f CMakeFiles/Makefile2 staticlib
  .PHONY : staticlib

  # fast build rule for target.
  staticlib/fast:
    $(MAKE) -f CMakeFiles/staticlib.dir/build.make CMakeFiles/staticlib.dir/build
  .PHONY : staticlib/fast

  program.o: program.c.o

  .PHONY : program.o

  # target to build an object file
  program.c.o:
    $(MAKE) -f CMakeFiles/dynamic_block.dir/build.make CMakeFiles/dynamic_block.dir/program.c.o
    $(MAKE) -f CMakeFiles/static_block.dir/build.make CMakeFiles/static_block.dir/program.c.o
  .PHONY : program.c.o

  program.i: program.c.i

  .PHONY : program.i

  # target to preprocess a source file
  program.c.i:
    $(MAKE) -f CMakeFiles/dynamic_block.dir/build.make CMakeFiles/dynamic_block.dir/program.c.i
    $(MAKE) -f CMakeFiles/static_block.dir/build.make CMakeFiles/static_block.dir/program.c.i
  .PHONY : program.c.i

  program.s: program.c.s

  .PHONY : program.s

  # target to generate assembly for a file
  program.c.s:
    $(MAKE) -f CMakeFiles/dynamic_block.dir/build.make CMakeFiles/dynamic_block.dir/program.c.s
    $(MAKE) -f CMakeFiles/static_block.dir/build.make CMakeFiles/static_block.dir/program.c.s
  .PHONY : program.c.s

  source/block.o: source/block.c.o

  .PHONY : source/block.o

  # target to build an object file
  source/block.c.o:
    $(MAKE) -f CMakeFiles/dynamiclib.dir/build.make CMakeFiles/dynamiclib.dir/source/block.c.o
    $(MAKE) -f CMakeFiles/staticlib.dir/build.make CMakeFiles/staticlib.dir/source/block.c.o
  .PHONY : source/block.c.o

  source/block.i: source/block.c.i

  .PHONY : source/block.i

  # target to preprocess a source file
  source/block.c.i:
    $(MAKE) -f CMakeFiles/dynamiclib.dir/build.make CMakeFiles/dynamiclib.dir/source/block.c.i
    $(MAKE) -f CMakeFiles/staticlib.dir/build.make CMakeFiles/staticlib.dir/source/block.c.i
  .PHONY : source/block.c.i

  source/block.s: source/block.c.s

  .PHONY : source/block.s

  # target to generate assembly for a file
  source/block.c.s:
    $(MAKE) -f CMakeFiles/dynamiclib.dir/build.make CMakeFiles/dynamiclib.dir/source/block.c.s
    $(MAKE) -f CMakeFiles/staticlib.dir/build.make CMakeFiles/staticlib.dir/source/block.c.s
  .PHONY : source/block.c.s

  # Help Target
  help:
    @echo "The following are some of the valid targets for this Makefile:"
    @echo "... all (the default if no target is provided)"
    @echo "... clean"
    @echo "... depend"
    @echo "... rebuild_cache"
    @echo "... edit_cache"
    @echo "... dynamiclib"
    @echo "... dynamic_block"
    @echo "... static_block"
    @echo "... staticlib"
    @echo "... program.o"
    @echo "... program.i"
    @echo "... program.s"
    @echo "... source/block.o"
    @echo "... source/block.i"
    @echo "... source/block.s"
  .PHONY : help



  #=============================================================================
  # Special targets to cleanup operation of make.

  # Special rule to run CMake to check the build system integrity.
  # No rule that depends on this can have commands that come from listfiles
  # because they might be regenerated.
  cmake_check_build_system:
    $(CMAKE_COMMAND) -S$(CMAKE_SOURCE_DIR) -B$(CMAKE_BINARY_DIR) --check-build-system CMakeFiles/Makefile.cmake 0
  .PHONY : cmake_check_build_system
  ```
* Difference in sizes
* Running ls -la revealed the dynamic program uses 16696 bytes while the static uses 160 fewer bytes at 16856 bytes. Cmake and the make file generated executables of the same size however cmake was nicer to use and I would definitely prefer it for larger projects.
* Output
  ![secondhalf](https://user-images.githubusercontent.com/49171429/174712444-e400e349-a123-4078-8c01-cb229784b2f6.png)

