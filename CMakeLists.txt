cmake_minimum_required (VERSION 3.7)
set(CMAKE_OSX_DEPLOYMENT_TARGET "10.13" CACHE STRING "Minimum OS X deployment version")

project(stun CXX)

cmake_policy(SET CMP0022 NEW)   # INTERFACE_LINK_LIBRARIES defines the link interface
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

message(STATUS "CMake Version: ${CMAKE_VERSION}")
message(STATUS "CMake Generator: ${CMAKE_GENERATOR}")
message(STATUS "CMake CXX Compiler ID: ${CMAKE_CXX_COMPILER_ID}")
message(STATUS "CMake CXX Compiler Version: ${CMAKE_CXX_COMPILER_VERSION}")
message(STATUS "CMake System: ${CMAKE_SYSTEM}")
message(STATUS "CMake System Processor: ${CMAKE_SYSTEM_PROCESSOR}")
message(STATUS "CMake Module Path: ${CMAKE_MODULE_PATH}")

add_compile_options("$<$<CONFIG:DEBUG>:-DDEBUG>")

file(GLOB common_SRC 		CONFIGURE_DEPENDS "common/*.h" "common/*.cpp")
file(GLOB stuncore_SRC 		CONFIGURE_DEPENDS "stuncore/*.h" "stuncore/*.cpp")
file(GLOB networkutils_SRC 	CONFIGURE_DEPENDS "networkutils/*.h" "networkutils/*.cpp")
file(GLOB testcode_SRC 		CONFIGURE_DEPENDS "testcode/*.h" "testcode/*.cpp")
file(GLOB client_SRC 		CONFIGURE_DEPENDS "client/*.h" "client/*.cpp")

set(server_SRC server/main.cpp
server/server.cpp
server/stunconnection.cpp
server/stunsocketthread.cpp
server/tcpserver.cpp)


include_directories(common stuncore networkutils testcode client server resources) 

add_executable(stunserver ${common_SRC} ${stuncore_SRC} ${networkutils_SRC} ${server_SRC} )
add_executable(stunclient ${common_SRC} ${stuncore_SRC} ${networkutils_SRC} ${client_SRC} )



