cmake_minimum_required(VERSION 3.4 FATAL_ERROR)
project(AwesomeProject LANGUAGES CXX)

set(AWESOMEPROJECT_MAJOR_VERSION 0)
set(AWESOMEPROJECT_MINOR_VERSION 1)
set(AWESOMEPROJECT_PATCH_VERSION 0)
set(AWESOMEPROJECT_VERSION
  ${AWESOMEPROJECT_MAJOR_VERSION}.${AWESOMEPROJECT_MINOR_VERSION}.${AWESOMEPROJECT_PATCH_VERSION})
message("[AWESOMEPROJECT_VERSION] ${AWESOMEPROJECT_VERSION}")


# Setup basic install PATHs for lib, bin, include and CMake
set(INSTALL_LIB_DIR lib CACHE PATH "Installation directory for libraries")
set(INSTALL_BIN_DIR bin CACHE PATH "Installation directory for executables")
set(INSTALL_INCLUDE_DIR include CACHE PATH
  "Installation directory for header files")
if(WIN32 AND NOT CYGWIN)
  set(DEF_INSTALL_CMAKE_DIR CMake)
else()
  set(DEF_INSTALL_CMAKE_DIR lib/CMake/${CMAKE_PROJECT_NAME})
endif()
set(INSTALL_CMAKE_DIR ${DEF_INSTALL_CMAKE_DIR} CACHE PATH
  "Installation directory for CMake files")

# Make relative install paths absolute (needed later on)
foreach(p LIB BIN INCLUDE CMAKE)
  message("For ${p} in (LIB, BIN, INCLUDE, CMAKE)")
  set(var INSTALL_${p}_DIR)
  message("[basic install path] ${${var}}")
  if(NOT IS_ABSOLUTE "${${var}}")
    # message("${CMAKE_INSTALL_PREFIX}/${${var}}")
    set(${var} "${CMAKE_INSTALL_PREFIX}/${${var}}")
    message("[absolute install path] ${${var}}")
  endif()
endforeach()

# set up include-directories
include_directories(
  "${PROJECT_SOURCE_DIR}/source"
  "${PROJECT_BINARY_DIR}")
# print include directories
get_property(dirs DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
  message(STATUS "dir='${dir}'")
endforeach()

# Targets that we develop here
add_subdirectory(source)
