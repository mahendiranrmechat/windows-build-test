cmake_minimum_required(VERSION 3.14)

project(runner LANGUAGES CXX)

set(BINARY_NAME "g_project")

# Define the executable with correct relative paths
add_executable(${BINARY_NAME}
  "runner/main.cpp"
  "runner/runner.rc"
)

# Windows-specific properties
set_target_properties(${BINARY_NAME} PROPERTIES
  WIN32_EXECUTABLE TRUE
  VS_DEBUGGER_WORKING_DIRECTORY "$<TARGET_FILE_DIR:${BINARY_NAME}>"
)

# Link Flutter and wrapper plugin
target_link_libraries(${BINARY_NAME} PRIVATE flutter flutter_wrapper_plugin)

# Include runner/ folder for headers
target_include_directories(${BINARY_NAME} PRIVATE
  "${CMAKE_CURRENT_SOURCE_DIR}/runner"
)
