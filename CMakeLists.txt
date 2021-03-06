cmake_minimum_required(VERSION 3.7.2)

project(libconfig)
option(BUILD_EXAMPLES "Enable examples" OFF)
option(BUILD_SHARED_LIBS  "Enable shared library" ON)
option(BUILD_TESTS "Enable tests" OFF)

set_property(GLOBAL	PROPERTY USE_FOLDERS ON)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/out)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/out)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/out)

if(BUILD_SHARED_LIBS)
	add_definitions(-DLIBCONFIG_EXPORTS)
	add_definitions(-DLIBCONFIGXX_EXPORTS)
else()
	add_definitions(-DLIBCONFIG_STATIC)
	add_definitions(-DLIBCONFIGXX_STATIC)
endif()

include(GNUInstallDirs)
add_subdirectory(lib)

if(BUILD_EXAMPLES)
	add_subdirectory(examples)
endif()

if(BUILD_TESTS)
	enable_testing()
	add_subdirectory(tinytest)
	add_subdirectory(tests)
endif()
