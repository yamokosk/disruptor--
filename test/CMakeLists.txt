# Library requires pthreads
find_package(Threads)

# Unit testing uses Boost
find_package(Boost COMPONENTS unit_test_framework REQUIRED)

add_executable(sequencer_test sequencer_test.cc)
target_link_libraries(sequencer_test ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY} ${CMAKE_THREAD_LIBS_INIT})
add_test(sequencer_test sequencer_test)

add_executable(ring_buffer_test ring_buffer_test.cc)
target_link_libraries(ring_buffer_test ${Boost_UNIT_TEST_FRAMEWORK_LIBRARY} ${CMAKE_THREAD_LIBS_INIT})
add_test(ring_buffer_test ring_buffer_test)