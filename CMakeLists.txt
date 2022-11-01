cmake_minimum_required(VERSION 3.18)
project(cpp-library-template)

set(CMAKE_CXX_STANDARD 20)

set(${PROJECT_NAME}_BUILD_EXAMPLES OFF CACHE BOOL "Include examples?")

message(STATUS ${PROJECT_NAME}_BUILD_EXAMPLES)

# Set build type if not set.
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
endif()

message(STATUS "Build type: ${CMAKE_BUILD_TYPE}")

if(CMAKE_BUILD_TYPE MATCHES Debug)
    message(STATUS "Build flags: ${CMAKE_CXX_FLAGS_DEBUG}")
else()
    message(STATUS "Build flags: ${CMAKE_CXX_FLAGS_RELEASE}")
endif()

message(STATUS "Using compiler: ${CMAKE_CXX_COMPILER_ID}")

if(CMAKE_CXX_COMPILER_ID MATCHES "Clang" )
    #set to see all warnings
    set(CMAKE_CXX_FLAGS "-Wall -Wextra")
elseif(MSVC)
    #set to see all warnings and if windows set exception handling mode to sc [https://docs.microsoft.com/en-us/cpp/build/reference/eh-exception-handling-model?view=msvc-170]
    set(CMAKE_CXX_FLAGS "-EHsc")
endif()

# Find and include packages
# find_package(package_name REQUIRED)
# message(STATUS "package_name include dirs: ${package_name_INCLUDE_DIRS}")

# Library implementation in src
add_subdirectory(src)

target_include_directories(${PROJECT_NAME} PUBLIC
    "include"
    "dependencies"
    # ${package_name_INCLUDE_DIRS}
)

# Include external dependencies
add_subdirectory(dependencies)

# Build sample project
if (${PROJECT_NAME}_BUILD_EXAMPLES)
    message(STATUS "Including examples")
    add_subdirectory(samples)
endif()

# keep enable_testing command in the source directory root because ctest expects to find a test file in the build directory root.
# enable_testing() 

# Test configuration in the test folder
# add_subdirectory(tests)