cmake_minimum_required(VERSION 3.20)

project(
    liburing_cmake
    VERSION 0.1
    LANGUAGES CXX
)

include(ExternalProject)

ExternalProject_Add(
    liburing_git
    GIT_REPOSITORY https://github.com/axboe/liburing.git
    GIT_TAG liburing-2.1
    GIT_PROGRESS 1
    CONFIGURE_COMMAND ./configure
    BUILD_COMMAND make
    BUILD_IN_SOURCE 1
    BUILD_BYPRODUCTS "<SOURCE_DIR>/src/liburing.a"
    INSTALL_COMMAND ""
    TEST_COMMAND ""
    LOG_CONFIGURE ON
    LOG_BUILD ON
    LOG_MERGED_STDOUTERR ON
    LOG_OUTPUT_ON_FAILURE ON
)

ExternalProject_Get_Property(liburing_git SOURCE_DIR)

add_library(liburing INTERFACE)

add_dependencies(liburing liburing_git)

target_include_directories(liburing INTERFACE
    ${SOURCE_DIR}/src/include
)

target_link_libraries(liburing INTERFACE
    "${SOURCE_DIR}/src/liburing.a"
)
