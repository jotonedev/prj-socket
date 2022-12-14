cmake_minimum_required(VERSION 3.16)
project(hangman_game CXX)

enable_language(C CXX)

set(CMAKE_C_STANDARD 20)
set(CMAKE_CXX_STANDARD 20)
set(INCLUDE_DIR ${CMAKE_SOURCE_DIR}/lib)
set(HANGMAN_LIB ${INCLUDE_DIR}/Hangman)


if (MINGW)
    set(CMAKE_CXX_STANDARD_LIBRARIES "-static-libgcc -static-libstdc++ ${CMAKE_CXX_STANDARD_LIBRARIES}")
endif ()


include_directories(${INCLUDE_DIR})

set(HANGMAN_CLIENT ${HANGMAN_LIB}/protocol.h ${HANGMAN_LIB}/client.h ${HANGMAN_LIB}/client.cpp ${HANGMAN_LIB}/terminal_utils.h)
set(HANGMAN_SERVER ${HANGMAN_LIB}/protocol.h ${HANGMAN_LIB}/server.h ${HANGMAN_LIB}/server.cpp ${HANGMAN_LIB}/string_utils.h)

add_library(hangman_client OBJECT ${HANGMAN_BASE} ${HANGMAN_CLIENT})
add_library(hangman_server OBJECT ${HANGMAN_BASE} ${HANGMAN_SERVER})


add_subdirectory(client)
add_subdirectory(server)
