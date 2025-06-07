

set(PROJECT_NAME new_project_name)
IF(ESP_PLATFORM)
    # build for ESP target
    set(SOURCES
        src/main.c
    )

    idf_component_register(SRCS
        ${SOURCES}
        INCLUDE_DIRS
        inc
        src
        libs
        REQUIRES
        
    )

ELSE()
    # build under normal CMake
    cmake_minimum_required(VERSION 3.16)
    project(${PROJECT_NAME} VERSION 0.0.1 DESCRIPTION "New project description" LANGUAGES C)
    add_library(${PROJECT_NAME} STATIC
        src/main.c
    )
    set_target_properties(${PROJECT_NAME} PROPERTIES VERSION ${PROJECT_VERSION})

    target_include_directories(${PROJECT_NAME} PRIVATE ./libs)
    target_include_directories(${PROJECT_NAME} PRIVATE ./src)
    target_include_directories(${PROJECT_NAME} PUBLIC ./inc)
ENDIF()
