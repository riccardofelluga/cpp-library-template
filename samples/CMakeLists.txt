#tell cmake where to put output binaries
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
message(STATUS "Output directory for sample: ${EXECUTABLE_OUTPUT_PATH}")

# add the main executable
add_executable(${PROJECT_NAME}_sample main.cpp)
target_link_libraries(${PROJECT_NAME}_sample PUBLIC ${PROJECT_NAME})
