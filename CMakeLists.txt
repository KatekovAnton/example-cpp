cmake_minimum_required(VERSION 3.14.0)
set(CMAKE_CXX_STANDARD 17)
set(PROJECT_NAME example_cpp)
set(TARGET_NAME ${PROJECT_NAME})
project(${PROJECT_NAME} C CXX)



# IF(APPLE)
#     SET (PROJECT_OS_MACOS TRUE BOOL INTERNAL)
#     add_definitions(-DPROJECT_TARGET_OS_MAC )
# ENDIF (APPLE)
# IF(WIN32)
#     SET (PROJECT_OS_WIN32 TRUE BOOL INTERNAL)
#     add_definitions(-DPROJECT_TARGET_OS_WIN )
# ENDIF (WIN32)
# if(UNIX AND NOT APPLE) 
#     SET (PROJECT_OS_LINUX TRUE BOOL INTERNAL)
#     add_definitions(-DPROJECT_TARGET_OS_LINUX )
# ENDIF (UNIX AND NOT APPLE)



# platform-independant sources
set(SRC_DIR "${PROJECT_SOURCE_DIR}/src")
include_directories("${SRC_DIR}")
include_directories("${SRC_DIR}/platform")

file(GLOB_RECURSE PROJECT_SOURCES 
    ${SRC_DIR}/*.cpp
    ${SRC_DIR}/*.hpp
    ${SRC_DIR}/*.h
)



if(CMAKE_GENERATOR STREQUAL Xcode)

    add_executable(${PROJECT_NAME} MACOSX_BUNDLE 
        ${PROJECT_SOURCES})

elseif(PROJECT_OS_MACOS)

    set(CMAKE_OSX_DEPLOYMENT_TARGET "10.14")
    add_executable(${PROJECT_NAME} MACOSX_BUNDLE 
        ${PROJECT_SOURCES})

elseif(WIN32)

    add_executable(${PROJECT_NAME} 
        ${PROJECT_SOURCES})
        
else ()

    add_executable(${PROJECT_NAME} ${PROJECT_SOURCES})
    
endif()
