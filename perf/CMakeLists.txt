# Library requires pthreads
find_package(Threads)

set(CMAKE_CXX_FLAGS "-O3 -DNDEBUG ${CMAKE_CXX_FLAGS}")

add_executable(perf-1P-1EP-UNICAST
				one_publisher_to_one_unicast_throughput_test.cc)
target_link_libraries(perf-1P-1EP-UNICAST ${CMAKE_THREAD_LIBS_INIT})

add_executable(perf_1P_3EP_PIPELINE_SOURCES
				one_publisher_to_three_pipeline_throughput_test.cc)
target_link_libraries(perf_1P_3EP_PIPELINE_SOURCES ${CMAKE_THREAD_LIBS_INIT})