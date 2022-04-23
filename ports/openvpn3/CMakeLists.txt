cmake_minimum_required(VERSION 3.5)
project(openvpncli CXX)

find_path(ASIO_HPP asio.hpp)
find_library(CRYPTO_LIB libcrypto)
find_library(SSL_LIB libssl)
find_library(LZ_LIB lz4)
find_library(JSONCPP_LIB jsoncpp)

include_directories(. ${ASIO_HPP})

if(WIN32) 
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /bigobj")
endif()

add_definitions(-DNOMINMAX -DUSE_ASIO -DUSE_OPENSSL -D_WIN32_WINNT=0x0600)

add_library(ovpncli client/ovpncli.cpp)
target_link_libraries(ovpncli PRIVATE Iphlpapi.lib Wininet.lib Setupapi.lib Cfgmgr32.lib Rpcrt4.lib Fwpuclnt.lib Wtsapi32.lib ${CRYPTO_LIB} ${SSL_LIB} ${LZ_LIB} ${JSONCPP_LIB})

install(
    TARGETS ovpncli
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
)

if(BUILD_TOOL)
    add_executable(cli test/ovpncli/cli.cpp)
    target_compile_definitions(cli PRIVATE -DTAP_WIN_COMPONENT_ID=tap0901)
    target_link_libraries(cli PRIVATE ovpncli)    
endif()