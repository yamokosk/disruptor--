cmake_minimum_required(VERSION 2.4.6)
project("disruptor")

# Enable CTest
include(CTest)

# The version number.
set(disruptor_VERSION_MAJOR 0)
set(disruptor_VERSION_MINOR 1)

# Process config.h
configure_file(
  "${PROJECT_SOURCE_DIR}/disruptor/config.h.in"
  "${PROJECT_BINARY_DIR}/disruptor/config.h"
)

# Add '-I{current_src_directory}'
include_directories(${PROJECT_SOURCE_DIR})
include_directories(${PROJECT_BINARY_DIR}) # to find generated config.h

# Compiler specific flags
if (CMAKE_COMPILER_IS_GNUCC)
	# Currently only tested with GCC.. specifically versions that support
	# C++0x or C++11.
    execute_process(COMMAND ${CMAKE_C_COMPILER} -dumpversion OUTPUT_VARIABLE GCC_VERSION)
    string(REGEX MATCHALL "[0-9]+" GCC_VERSION_COMPONENTS ${GCC_VERSION})
    list(GET GCC_VERSION_COMPONENTS 0 GCC_MAJOR)
    list(GET GCC_VERSION_COMPONENTS 1 GCC_MINOR)

    # gcc >= 4.6?
    if ( (NOT (${GCC_MAJOR} LESS 4)) AND (NOT (${GCC_MINOR} LESS 6)) )
    	# gcc >= 4.7?
    	if (NOT (${GCC_MINOR} LESS 7))
    		set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")
    	else()
    		set(CMAKE_CXX_FLAGS "-std=c++0x ${CMAKE_CXX_FLAGS}")
    	endif()
    else()
    	message(FATAL_ERROR "disruptor requires GCC (version >= 4.6). Found GCC v${GCC_MAJOR}.${GCC_MINOR}")
    endif()
else()
	message(FATAL_ERROR "disruptor-- has only been tested with GCC")
endif()

# library relies on C++0x
add_subdirectory(perf)
add_subdirectory(test)