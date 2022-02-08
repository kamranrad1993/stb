cmake_minimum_required(VERSION 3.2)

set(CMAKE_CONFIGURATION_TYPES "Debug;Dev;Release"
    CACHE STRING
    "List of supported configurations."
    FORCE)

project(stb)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

if( PLATFORM_WINDOWS )
	add_compile_options(-DWINDOWSPC)
endif()


# Initialize the development configuration using release configuration
set(CMAKE_C_FLAGS_DEV "${CMAKE_C_FLAGS_RELEASE}")
set(CMAKE_CXX_FLAGS_DEV "${CMAKE_CXX_FLAGS_RELEASE}")
set(CMAKE_STATIC_LINKER_FLAGS_DEV "${CMAKE_STATIC_LINKER_FLAGS_RELEASE}")

set(root ${CMAKE_CURRENT_SOURCE_DIR})
file(GLOB ALL_SOURCE_FILES ${root}/*.h ${root}/*.c ${root}/*.cpp ${root}/*.hpp)

add_library(${PROJECT_NAME} STATIC ${ALL_SOURCE_FILES})

install(FILES ${ALL_SOURCE_FILES} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

