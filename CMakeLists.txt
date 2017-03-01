cmake_minimum_required(VERSION 2.8.3)
project(serial)


include_directories(include)
add_subdirectory( src )

## Uncomment for example
add_executable(serial_example examples/serial_example.cc)
add_dependencies(serial_example ${PROJECT_NAME})
target_link_libraries(serial_example ${PROJECT_NAME})


#add_subdirectory( tests )
