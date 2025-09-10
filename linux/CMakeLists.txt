cmake_minimum_required(VERSION 3.10)

set(PROJECT_NAME "disk_space_2")
project(${PROJECT_NAME} LANGUAGES CXX)

set(PLUGIN_NAME "disk_space_2_plugin")

# Source files
list(APPEND PLUGIN_SOURCES
  "disk_space_2_plugin.cc"
)

# Create the shared library
add_library(${PLUGIN_NAME} SHARED
  ${PLUGIN_SOURCES}
)

# Flutter standard settings
apply_standard_settings(${PLUGIN_NAME})

set_target_properties(${PLUGIN_NAME} PROPERTIES
  CXX_VISIBILITY_PRESET hidden)

target_compile_definitions(${PLUGIN_NAME} PRIVATE FLUTTER_PLUGIN_IMPL)

# Include plugin headers
target_include_directories(${PLUGIN_NAME} INTERFACE
  "${CMAKE_CURRENT_SOURCE_DIR}/include"
)

# Link with flutter and GTK (if needed)
find_package(PkgConfig REQUIRED)
pkg_check_modules(GTK REQUIRED gtk+-3.0)

target_include_directories(${PLUGIN_NAME} PRIVATE
  ${GTK_INCLUDE_DIRS}
)

target_compile_options(${PLUGIN_NAME} PRIVATE ${GTK_CFLAGS_OTHER})

target_link_libraries(${PLUGIN_NAME} PRIVATE
  flutter
  ${GTK_LIBRARIES}
)

# Bundled libraries placeholder
set(disk_space_2_bundled_libraries
  ""
  PARENT_SCOPE
)
