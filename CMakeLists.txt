cmake_minimum_required(VERSION 3.12 FATAL_ERROR)

if(NOT DEFINED PROJECT_NAME)
  set(OPTIONS_NOT_SUBPROJECT ON)
endif()

project(options VERSION 1.0 LANGUAGES CXX)

if(NOT CMAKE_BUILD_TYPE)
  message(STATUS "Setting build type to Release as none was specified.")
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY VALUE "Release")
endif()

add_library(options SHARED ${options_SOURCE_DIR}/src/options.cpp)
target_include_directories(options PUBLIC 
  $<BUILD_INTERFACE:${options_SOURCE_DIR}/src>
  )
target_compile_features(cosma PUBLIC cxx_std_11)

if(OPTIONS_NOT_SUBPROJECT)
  install(TARGETS options
          EXPORT options_targets 
          LIBRARY DESTINATION lib
          INCLUDES DESTINATION include)

  install(EXPORT options_targets
          FILE optionsConfig.cmake
          NAMESPACE options::
          DESTINATION lib/cmake/options)

  install(FILES src/options.hpp
          DESTINATION include)

  include(CMakePackageConfigHelpers)
  write_basic_package_version_file(
    "${options_BINARY_DIR}/optionsConfigVersion.cmake"
    VERSION ${options_VERSION}
    COMPATIBILITY SameMajorVersion)

  install(FILES "${options_BINARY_DIR}/optionsConfigVersion.cmake"
          DESTINATION lib/cmake/options)
endif()

if(OPTIONS_NOT_SUBPROJECT)
  add_subdirectory(examples)
endif()
