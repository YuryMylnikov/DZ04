cmake_minimum_required(VERSION 3.2)

if($ENV{TRAVIS_BUILD_NUMBER})
    set(VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})
    message("=====TRUE====")
else()
    set(VERSION 0.0.0)
    message("=====FALSE====")
endif()

message("=====TRAVIS_BUILD_NUMBER==== ${TRAVIS_BUILD_NUMBER}")
message("=====VERSION==== ${VERSION}")

project(print_ip VERSION ${VERSION})

add_executable(print_ip print_ip.cpp)

set_target_properties(print_ip  PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
)

set(CMAKE_CXX_STANDARD 17)

if (MSVC)
    target_compile_options(print_ip PRIVATE
        /W4
    )
else ()
    target_compile_options(print_ip PRIVATE
        -Wall -Wextra -pedantic -Werror
    )
endif()

install(TARGETS print_ip RUNTIME DESTINATION bin)

set(CPACK_GENERATOR DEB)

set(CPACK_PACKAGE_CONTACT example@example.com)

include(CPack)