cmake_minimum_required(VERSION 3.0.0)
project(libssh_demo VERSION 0.1.0)

include(CTest)
enable_testing()

find_package(libssh REQUIRED)
if (NOT TARGET ssh)
     add_library(ssh SHARED IMPORTED)
     set_target_properties(ssh
                           PROPERTIES
                 ​          IMPORTED_LOCATION "${LIBSSH_LIBRARIES}"
                           INTERFACE_INCLUDE_DIRECTORIES "${LIBSSH_INCLUDE_DIR}")
endif()

add_executable(libssh_demo main.cpp)

target_link_libraries(libssh_demo PRIVATE 
ssh
)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
