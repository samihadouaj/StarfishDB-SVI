#
# Usage:
#
# *  For DEBUG builds: 
#    > cd build
#    > cmake3 -DCMAKE_BUILD_TYPE=Debug -D CMAKE_C_COMPILER=gcc -D CMAKE_CXX_COMPILER=g++ ..
#    > make clean && make
#
#
# *  For RELEASE builds: 
#    > cd build
#    > cmake3 -DCMAKE_BUILD_TYPE=RelWithDebInfo -D CMAKE_C_COMPILER=gcc -D CMAKE_CXX_COMPILER=g++ ..
#    > make clean && make
#
#
cmake_minimum_required(VERSION 3.5.1)

project(lda_wiki_preprocess)

# when in doubt, do a RELEASE build but keep the debug symbols
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE RelWithDebInfo)
endif()

set(CMAKE_CXX_STANDARD 20)           # c++20
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# generate verbose Makefile
set(CMAKE_VERBOSE_MAKEFILE ON)

add_compile_options(
  -Wall -Wextra -ggdb3 -march=native#-rdynamic
  $<$<CONFIG:RELEASE>:-O3>
  $<$<CONFIG:RELWITHDEBINFO>:-O3>
  $<$<CONFIG:DEBUG>:-O0>
)

add_compile_definitions(
  $<$<CONFIG:RELEASE>:NDEBUG>
  $<$<CONFIG:RELWITHDEBINFO>:NDEBUG>
  $<$<CONFIG:DEBUG>:DEBUG>
)

# declare source files
set(SRCS

# src
  src/lda_wiki_preprocess.cpp
  src/clean.cpp
  src/clean.h
  src/Vocabulary.cpp
  src/Vocabulary.h
  # Utils
  src/Utils/argparse.hpp
  src/Utils/DebugHelper.h
  src/Utils/TimeThis.cpp
  src/Utils/TimeThis.h
  src/Utils/RndUtils.cpp
  src/Utils/RndUtils.h
)
 
# declare dependencies
#find_package(OpenMP REQUIRED)

# declare executables
add_executable(lda_wiki_preprocess src/lda_wiki_preprocess.cpp ${SRCS})


