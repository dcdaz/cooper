cmake_minimum_required(VERSION 3.30 FATAL_ERROR)
INCLUDE(CheckCXXCompilerFlag)

project("Cooper")

CHECK_CXX_COMPILER_FLAG(-std=c++23 COMPILER_SUPPORTS_CXX23)
IF (COMPILER_SUPPORTS_CXX23)
    ADD_COMPILE_OPTIONS("-std=c++23")
ELSE ()
    MESSAGE(FATAL_ERROR "Compiler ${CMAKE_CXX_COMPILER} has no C++23 support.")
ENDIF ()

ADD_COMPILE_OPTIONS("-Wall" "-Wextra" "-Wpedantic" "-Werror")
set(CMAKE_CXX_STANDARD 23)

function(cooper_tests test_name)
    add_executable(${test_name}_exec ${test_name}.cpp)
    add_test(NAME ${test_name} COMMAND ${test_name}_exec)
    target_compile_features(${test_name}_exec
        PRIVATE
            cxx_auto_type
        PUBLIC
            cxx_nullptr
            cxx_override
    )
endfunction()

cooper_tests(stringutils_test)
cooper_tests(config_test)
