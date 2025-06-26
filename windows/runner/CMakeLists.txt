cmake_minimum_required(VERSION 3.14)

project(runner LANGUAGES CXX)

set(BINARY_NAME "g_project")

add_executable(${BINARY_NAME}
  "main.cpp"
  "runner.rc"
)

set_target_properties(${BINARY_NAME} PROPERTIES
  WIN32_EXECUTABLE TRUE
  VS_DEBUGGER_WORKING_DIRECTORY "$<TARGET_FILE_DIR:${BINARY_NAME}>"
)

target_include_directories(${BINARY_NAME} PRIVATE
  "${CMAKE_CURRENT_SOURCE_DIR}"
)

target_sources(${BINARY_NAME} PRIVATE
  "${CMAKE_CURRENT_BINARY_DIR}/flutter/generated_plugin_registrant.cc"
)

# === Inline settings (fix for missing apply_standard_settings) ===
target_compile_features(${BINARY_NAME} PUBLIC cxx_std_17)
target_compile_options(${BINARY_NAME} PRIVATE /W4 /WX /wd"4100")
target_compile_options(${BINARY_NAME} PRIVATE /EHsc)
target_compile_definitions(${BINARY_NAME} PRIVATE "_HAS_EXCEPTIONS=0")
target_compile_definitions(${BINARY_NAME} PRIVATE "$<$<CONFIG:Debug>:_DEBUG>")
# =================================================================

target_link_libraries(${BINARY_NAME} PRIVATE flutter flutter_wrapper_plugin)
