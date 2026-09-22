#learnt from https://cliutils.gitlab.io/modern-cmake/basics/

cmake_minimum_required(VERSION 4.2) #initial cmake setup and version enforcement.
#Maximum version gone?

set(CMAKE_CXX_STANDARD 20) #/
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

message(STATUS "CMake Version: ${CMAKE_VERSION}") #/

set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Release>:Release>") #These lines come highly reccomended by LowLevelGameDev; 
set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>") #/

file(GLOB_RECURSE LEARN_INCLUDE ${PROJECT_SOURCE_DIR}/MyApp/include/*.h)

project(VulkanLearning VERSION 0.00 DESCRIPTION "Just testing Vulkan" LANGUAGES CXX)


#We could put this lower if we wanted to have like "Project/src" but for now this does.
file(GLOB_RECURSE CRUMB_SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")


#If we are testing, we want to include the "tests" directory... this will open up the
if(CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME AND BUILD_TESTING)
    add_subdirectory(tests)
endif()

add_executable(VulkanTesting ${VT_Include} ${VT_Source})