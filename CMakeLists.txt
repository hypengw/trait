cmake_minimum_required(VERSION 3.28)
project(
  trait
  VERSION 0.1.0
  DESCRIPTION "rust like trait for c++"
  LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

option(RC_BUILD_TESTS "Build tests" ${PROJECT_IS_TOP_LEVEL})

add_library(trait)
add_library(rstd::trait ALIAS trait)
target_sources(
  trait
  PUBLIC FILE_SET
         all
         TYPE
         CXX_MODULES
         BASE_DIRS
         src
         FILES
         src/trait.cppm)

# Add installation rules
if(PROJECT_IS_TOP_LEVEL)
  include(GNUInstallDirs)
  install(
    TARGETS trait
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()

# Testing configuration
if(RC_BUILD_TESTS)
  include(CTest)
  enable_testing()
  add_subdirectory(test)
endif()
