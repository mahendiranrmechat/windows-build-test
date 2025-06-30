cmake_minimum_required(VERSION 3.14)

project(runner LANGUAGES CXX)

set(BINARY_NAME "g_project")

# Define the executable
add_executable(${BINARY_NAME}
  "main.cpp"
  "runner.rc"
)

# Set Windows-specific properties
set_target_properties(${BINARY_NAME} PROPERTIES
  WIN32_EXECUTABLE TRUE
  VS_DEBUGGER_WORKING_DIRECTORY "$<TARGET_FILE_DIR:${BINARY_NAME}>"
)

# Link Flutter and wrapper plugin
# ⚠️ Make sure flutter_wrapper_plugin is defined in your Flutter build setup
target_link_libraries(${BINARY_NAME} PRIVATE flutter flutter_wrapper_plugin)

# Include headers
target_include_directories(${BINARY_NAME} PRIVATE
  "${CMAKE_CURRENT_SOURCE_DIR}"
)

# Generated plugin registrant (optional — Flutter auto-generates this)
# Add the generated_plugin_registrant.cc or .cpp if needed
file(GLOB_RECURSE FLUTTER_GENERATED_SRC
  "${CMAKE_CURRENT_SOURCE_DIR}/generated_plugin_registrant.cc"
)

target_sources(${BINARY_NAME} PRIVATE ${FLUTTER_GENERATED_SRC})
