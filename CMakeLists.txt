cmake_minimum_required (VERSION 2.8)
project (DieStaemme)

# create "compile_commands.json"
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

# add some c++ flags
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Werror -std=c++1z")

include_directories("server/include")
include_directories("client/include")

set(CMAKE_PREFIX_PATH "${CMAKE_SOURCE_DIR/libs}" ${CMAKE_PREFIX_PATH})

set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}" ${CMAKE_MODULE_PATH})
find_package(SFML 2 REQUIRED system window graphics)
find_package(SFGUI REQUIRED)

include_directories(${SFML_INCLUDE_DIR})
include_directories(${SFGUI_INCLUDE_DIR})

file(GLOB src_files_client
    "client/include/*.hpp"
    "client/src/*.cpp"
)

file(GLOB src_files_server
    "server/include/*.hpp"
    "server/src/*.cpp"
)

add_executable(ds_client ${src_files_client})
target_link_libraries(ds_client ${SFML_LIBRARIES})
target_link_libraries(ds_client ${SFGUI_LIBRARY})

add_executable(ds_server ${src_files_server})
