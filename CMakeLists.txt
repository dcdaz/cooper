cmake_minimum_required(VERSION 3.30 FATAL_ERROR)
INCLUDE(CheckCXXCompilerFlag)

project("Cooper")

include_directories(${PROJECT_SOURCE_DIR}/src)

CHECK_CXX_COMPILER_FLAG(-std=c++23 COMPILER_SUPPORTS_CXX23)
IF (COMPILER_SUPPORTS_CXX23)
    ADD_COMPILE_OPTIONS("-std=c++23")
ELSE ()
    MESSAGE(FATAL_ERROR "Compiler ${CMAKE_CXX_COMPILER} has no C++23 support.")
ENDIF ()

ADD_COMPILE_OPTIONS("-Wall" "-Wextra" "-Wpedantic" "-Werror" )

set(CMAKE_CXX_STANDARD 23)

add_executable(cooper src/main.cpp)
target_link_libraries(cooper sqlite3)

enable_testing()
add_subdirectory(test)
