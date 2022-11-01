# cpp-library-template config

set(SOURCES
    lib.cpp
)

add_library(${PROJECT_NAME} STATIC ${SOURCES})

# link dependencies and packages
# target_link_libraries(${PROJECT_NAME} PUBLIC dependency_name ${package_name_LIBRARIES})