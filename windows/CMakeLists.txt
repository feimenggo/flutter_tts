cmake_minimum_required(VERSION 3.14)

if(POLICY CMP0153)
    cmake_policy(SET CMP0153 NEW)
endif()

set(PROJECT_NAME "flutter_tts")
project(${PROJECT_NAME} LANGUAGES CXX)

set(PLUGIN_NAME "flutter_tts_plugin")

add_library(${PLUGIN_NAME} SHARED
        "flutter_tts_plugin.cpp"
)

apply_standard_settings(${PLUGIN_NAME})

set_target_properties(${PLUGIN_NAME} PROPERTIES
        CXX_VISIBILITY_PRESET hidden
        VISIBILITY_INLINES_HIDDEN YES
)

target_compile_definitions(${PLUGIN_NAME} PRIVATE FLUTTER_PLUGIN_IMPL)

target_include_directories(${PLUGIN_NAME} INTERFACE
        "${CMAKE_CURRENT_SOURCE_DIR}/include"
)

target_link_libraries(${PLUGIN_NAME} PRIVATE
        flutter
        flutter_wrapper_plugin
)

set(flutter_tts_bundled_libraries "" PARENT_SCOPE)