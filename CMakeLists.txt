cmake_minimum_required(VERSION 3.17)
project(RtspProxyTestingOnLinux)

set(CMAKE_CXX_STANDARD 17)

find_package(OpenSSL REQUIRED SSL Crypto)

find_library(liveMediaLib liveMedia REQUIRED)
find_library(groupsockLib groupsock REQUIRED)
find_library(UsageEnvironmentLib UsageEnvironment REQUIRED)
find_library(BasicUsageEnvironmentLib BasicUsageEnvironment REQUIRED)

add_library(liveMedia STATIC IMPORTED)
set_target_properties(liveMedia PROPERTIES IMPORTED_LOCATION ${liveMediaLib})
add_library(groupsock STATIC IMPORTED)
set_target_properties(groupsock PROPERTIES IMPORTED_LOCATION ${groupsockLib})
add_library(UsageEnvironment STATIC IMPORTED)
set_target_properties(UsageEnvironment PROPERTIES IMPORTED_LOCATION ${UsageEnvironmentLib})
add_library(BasicUsageEnvironment STATIC IMPORTED)
set_target_properties(BasicUsageEnvironment PROPERTIES IMPORTED_LOCATION ${BasicUsageEnvironmentLib})

add_executable(RtspProxyTestingOnLinux main.cpp)
target_include_directories(RtspProxyTestingOnLinux PRIVATE ${OPENSSL_INCLUDE_DIR})
target_link_libraries(RtspProxyTestingOnLinux liveMedia BasicUsageEnvironment UsageEnvironment groupsock OpenSSL::SSL OpenSSL::Crypto)