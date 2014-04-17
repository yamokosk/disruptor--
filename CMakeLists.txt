cmake_minimum_required(VERSION 2.4.6)
project("disruptor--")

# Needs boost library
# set(Boost_USE_STATIC_LIBS OFF) 
# set(Boost_USE_MULTITHREADED ON)  
# set(Boost_USE_STATIC_RUNTIME OFF) 
# find_package(Boost 1.45.0 COMPONENTS *boost libraries here*) 

# if(Boost_FOUND)
#     include_directories(${Boost_INCLUDE_DIRS}) 
#     add_executable(progname file1.cxx file2.cxx) 
#     target_link_libraries(progname ${Boost_LIBRARIES})                                                                                                                                                                                                                            
# endif()

# Add '-I{current_src_directory}'
include_directories(.)

# library relies on C++0x
set(CMAKE_CXX_FLAGS "-std=c++0x ${CMAKE_CXX_FLAGS}")
set(CMAKE_EXE_LINKER_FLAGS "-pthread")

add_subdirectory(perf)
add_subdirectory(test)