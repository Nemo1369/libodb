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
set(APPLE_SIGN_IDENTITY "" CACHE STRING "Sign identity name")

set(CMAKE_OSX_ARCHITECTURES "$(ARCHS_STANDARD)" CACHE string "Build architecture")

if(${CMAKE_C_COMPILER_ID} MATCHES "Clang" OR ${CMAKE_CXX_COMPILER_ID} MATCHES "Clang")
    set(CMAKE_COMPILER_IS_CLANG TRUE)
endif()

if(CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX OR CMAKE_COMPILER_IS_CLANG)
    if(CMAKE_BUILD_TYPE MATCHES DEBUG)
        list(APPEND CMAKE_CXX_FLAGS "-g")
    endif()

    list(APPEND CMAKE_CXX_FLAGS "-Wall -Wextra -Wno-unused-function -Wno-unused-parameter -Werror-implicit-function-declaration -Wno-missing-field-initializers ${CMAKE_CXX_FLAGS} -fno-strict-aliasing -std=gnu++14")
    list(APPEND CMAKE_C_FLAGS "-Wall -Wextra -Wno-unused-function -Wno-unused-parameter  -Werror-implicit-function-declaration -Wno-missing-braces -Wno-missing-field-initializers ${CMAKE_C_FLAGS} -std=gnu99 -fno-strict-aliasing")

    option(USE_LIBC++ "Use libc++ instead of libstdc++" ${APPLE})
    if(USE_LIBC++)
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
    endif()
endif()

if(BUILD_UNIT_TESTS)
    enable_testing()
endif()

add_subdirectory(odb)
