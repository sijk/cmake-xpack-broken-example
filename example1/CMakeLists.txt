cmake_minimum_required(VERSION 3.26.5)
project(cmake-xpack-broken-example)

include(ExternalProject)
ExternalProject_Add(
    cmake-xpack
    GIT_REPOSITORY https://github.com/xpack-dev-tools/cmake-xpack
    GIT_TAG v3.26.5-1
    CONFIGURE_COMMAND ""
    BUILD_COMMAND ""
    INSTALL_COMMAND ""
)
