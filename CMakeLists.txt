cmake_minimum_required(VERSION 3.5)

project(HelloQt)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

# Must set 'CMAKE_PREFIX_PATH' for 'find_package()' to work
if(WIN32)
    set(CMAKE_PREFIX_PATH "C:/Qt/5.15.0/")
endif()

if(UNIX)
    set(CMAKE_PREFIX_PATH "~/Qt/5.15.0/gcc_64/")
endif()

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

find_package(Qt5Core REQUIRED)
find_package(Qt5Network REQUIRED)

add_executable("${PROJECT_NAME}"
    src/main.cpp
    src/worker.cpp
)

target_link_libraries("${PROJECT_NAME}"
    PRIVATE
        Qt5::Core
        Qt5::Network
)
