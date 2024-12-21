cmake_minimum_required(VERSION 3.8)

#
# COMPILER SETTINGS
#

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wno-psabi -rdynamic")
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -rdynamic")
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(THREADS_PREFER_PTHREAD_FLAG ON)

#
# SOURCE FILES
#

file(GLOB_RECURSE PROJ_SOURCES
    "*.h"
    "*.cpp"
)

#
# DEFAULT TARGET
#

add_executable(default_target ${PROJ_SOURCES})

set_property(TARGET default_target PROPERTY ENABLE_EXPORTS 1)

target_include_directories(default_target PUBLIC ${CMAKE_SOURCE_DIR})

set_target_properties(default_target PROPERTIES RUNTIME_OUTPUT_DIRECTORY
    ${CMAKE_SOURCE_DIR}/Result)


#
# PIPELINE TARGET
#

add_executable(pipeline_target ${PROJ_SOURCES})

set_property(TARGET pipeline_target PROPERTY ENABLE_EXPORTS 1)

target_include_directories(pipeline_target PUBLIC ${CMAKE_SOURCE_DIR})

set_target_properties(pipeline_target PROPERTIES RUNTIME_OUTPUT_DIRECTORY
    ${CMAKE_SOURCE_DIR}/Result)

target_compile_options(pipeline_target PRIVATE -Werror)