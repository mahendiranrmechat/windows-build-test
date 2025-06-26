cmake_minimum_required(VERSION 3.14)

project(runner LANGUAGES CXX)

set(BINARY_NAME "g_project")  # This should match the parent CMakeLists.txt

# Define the executable target with only existing source files
add_executable(${BINARY_NAME}
  "main.cpp"
  "runner.rc"
)

# Set properties
set_target_properties(${BINARY_NAME} PROPERTIES
  WIN32_EXECUTABLE TRUE
  VS_DEBUGGER_WORKING_DIRECTORY "$<TARGET_FILE_DIR:${BINARY_NAME}>"
)

# Link Flutter and other dependencies
target_link_libraries(${BINARY_NAME} PRIVATE flutter flutter_wrapper_plugin)

# Apply compile options and definitions from the parent
apply_standard_settings(${BINARY_NAME})

# Include headers
target_include_directories(${BINARY_NAME} PRIVATE
  "${CMAKE_CURRENT_SOURCE_DIR}"
)

# Generated plugin registrant
target_sources(${BINARY_NAME} PRIVATE
  "${CMAKE_CURRENT_BINARY_DIR}/flutter/generated_plugin_registrant.cc"
)
