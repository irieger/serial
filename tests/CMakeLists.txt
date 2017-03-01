if(UNIX)
    enable_testing()
    find_package(GTest REQUIRED)
    include_directories(${GTEST_INCLUDE_DIRS})


    add_executable(${PROJECT_NAME}-test unix_serial_tests.cc)
    target_link_libraries(${PROJECT_NAME}-test ${PROJECT_NAME} ${Boost_LIBRARIES} ${GTEST_BOTH_LIBRARIES})
    if(NOT APPLE)
        target_link_libraries(${PROJECT_NAME}-test util)
    endif()

    catkin_add_gtest(${PROJECT_NAME}-test-timer unit/unix_timer_tests.cc)
    target_link_libraries(${PROJECT_NAME}-test-timer ${PROJECT_NAME})
endif()
