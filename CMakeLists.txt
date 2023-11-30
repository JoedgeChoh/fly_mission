cmake_minimum_required(VERSION 3.10.2)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(fly_mission)
include_directories(thirdparty/yaml-cpp/include)
add_executable(fly_mission
    fly_mission.cpp
)

find_package(MAVSDK REQUIRED)
find_library(STATIC_LINK_LIB yaml-cpp PATHS ${PROJECT_SOURCE_DIR}/thirdparty/yaml-cpp/lib NO_DEFAULT_PATH)
if(STATIC_LINK_LIB)
    MESSAGE(STATUS "Found STATIC_LINK_LIB: ${STATIC_LINK_LIB}")
else()
    MESSAGE(STATUS "STATIC_LINK_LIB not found")
endif()

target_link_libraries(fly_mission
    MAVSDK::mavsdk ${STATIC_LINK_LIB}
)

if(NOT MSVC)
    add_compile_options(fly_mission PRIVATE -Wall -Wextra)
else()
    add_compile_options(fly_mission PRIVATE -WX -W2)
endif()
install(TARGETS fly_mission RUNTIME DESTINATION ${PROJECT_SOURCE_DIR})
