cmake_minimum_required(VERSION 2.8.12)

cmake_policy(SET CMP0042 NEW)
cmake_policy(SET CMP0048 NEW)

project(odb CXX C)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake" "${CMAKE_SOURCE_DIR}/cmake/modules")
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

if(MSVC AND NOT EXISTS "${CMAKE_BINARY_DIR}/ALL_BUILD.vcxproj.user")
    file(GENERATE
            OUTPUT "${CMAKE_BINARY_DIR}/ALL_BUILD.vcxproj.user"
            INPUT "${CMAKE_SOURCE_DIR}/cmake/ALL_BUILD.vcxproj.user.in"
            )
endif()

option(BUILD_UNIT_TESTS "Build unit tests" FALSE)
option(BUILD_SHARED_LIBRARIES "Build shared library version" TRUE)
set(APPLE_CODE_SIGN_IDENTITY "" CACHE STRING "Sign identity name")

set(CMAKE_OSX_ARCHITECTURES "$(ARCHS_STANDARD)" CACHE string "Build architecture")

if(${CMAKE_C_COMPILER_ID} MATCHES "Clang" OR ${CMAKE_CXX_COMPILER_ID} MATCHES "Clang")
    set(CMAKE_COMPILER_IS_CLANG TRUE)
endif()

if(CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX OR CMAKE_COMPILER_IS_CLANG)
    option(USE_LIBC++ "Use libc++ instead of libstdc++" ${APPLE})
endif()

configure_file(${PROJECT_SOURCE_DIR}/odb/details/config.h.in
    ${PROJECT_SOURCE_DIR}/odb/details/config.h)

if(BUILD_UNIT_TESTS)
    enable_testing()
endif()

add_subdirectory(odb)
