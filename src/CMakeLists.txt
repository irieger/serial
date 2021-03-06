set(SERIAL_LIB_NAME serial)


## Sources
set(serial_SRCS
    serial.cc
    ../include/serial/serial.h
    ../include/serial/v8stdint.h
)
if(APPLE)
	# If OSX
	list(APPEND serial_SRCS impl/unix.cc)
	list(APPEND serial_SRCS impl/list_ports/list_ports_osx.cc)
elseif(UNIX)
    # If unix
    list(APPEND serial_SRCS impl/unix.cc)
    list(APPEND serial_SRCS impl/list_ports/list_ports_linux.cc)
else()
    # If windows
    list(APPEND serial_SRCS impl/win.cc)
    list(APPEND serial_SRCS impl/list_ports/list_ports_win.cc)
endif()


## Add serial library
add_library(${SERIAL_LIB_NAME} ${serial_SRCS})

if(APPLE)
    find_library(IOKIT_LIBRARY IOKit)
    find_library(FOUNDATION_LIBRARY Foundation)
	target_link_libraries(${SERIAL_LIB_NAME} ${FOUNDATION_LIBRARY} ${IOKIT_LIBRARY})
elseif(UNIX)
	target_link_libraries(${SERIAL_LIB_NAME} rt pthread)
else()
	target_link_libraries(${SERIAL_LIB_NAME} setupapi)
endif()

install( TARGETS ${SERIAL_LIB_NAME} DESTINATION lib )
