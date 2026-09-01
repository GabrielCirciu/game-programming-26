cmake_minimum_required(VERSION 4.0)

project(gp26_exercises)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS})

set(BUILD_SHARED_LIBS OFF)

# 3rd party libraries
add_subdirectory(lib/SDL)

# repo's executables
add_subdirectory(examples)
add_subdirectory(playground)
add_subdirectory(exercises)
add_subdirectory(exercises_workplace)
add_subdirectory(exercises_solutions)

# ugly hack to avoid setting the working directory for VSCode (which works for debuggin only)
if(EXISTS ${CMAKE_SOURCE_DIR}/data)
    if(NOT EXISTS ${CMAKE_BINARY_DIR}/data)
        file(CREATE_LINK ${CMAKE_SOURCE_DIR}/data ${CMAKE_BINARY_DIR}/data SYMBOLIC RESULT link_res)
        if(NOT link_res EQUAL 0)
            file(COPY ${CMAKE_SOURCE_DIR}/data DESTINATION ${CMAKE_BINARY_DIR})
        endif()
    endif()

    if(EXISTS ${CMAKE_BINARY_DIR}/Debug AND NOT EXISTS ${CMAKE_BINARY_DIR}/Debug/data)
        file(CREATE_LINK ${CMAKE_SOURCE_DIR}/data ${CMAKE_BINARY_DIR}/Debug/data SYMBOLIC RESULT link_res_debug)
        if(NOT link_res_debug EQUAL 0)
            file(COPY ${CMAKE_SOURCE_DIR}/data DESTINATION ${CMAKE_BINARY_DIR}/Debug)
        endif()
    endif()

    if(EXISTS ${CMAKE_BINARY_DIR}/Release AND NOT EXISTS ${CMAKE_BINARY_DIR}/Release/data)
        file(CREATE_LINK ${CMAKE_SOURCE_DIR}/data ${CMAKE_BINARY_DIR}/Release/data SYMBOLIC RESULT link_res_release)
        if(NOT link_res_release EQUAL 0)
            file(COPY ${CMAKE_SOURCE_DIR}/data DESTINATION ${CMAKE_BINARY_DIR}/Release)
        endif()
    endif()
endif()

