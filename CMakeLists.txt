cmake_minimum_required(VERSION 3.15)
project(api-client)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Dependencies
add_subdirectory(external/json)

# Find system CURL
find_package(CURL REQUIRED)

# ImGui + GLFW + OpenGL
find_package(OpenGL REQUIRED)
find_package(glfw3 3.3 REQUIRED)

# Add ImGui source files
set(IMGUI_SOURCES
    external/imgui/imgui.cpp
    external/imgui/imgui_demo.cpp
    external/imgui/imgui_draw.cpp
    external/imgui/imgui_tables.cpp
    external/imgui/imgui_widgets.cpp
    external/imgui/backends/imgui_impl_glfw.cpp
    external/imgui/backends/imgui_impl_opengl3.cpp
)

# Main application
add_executable(${PROJECT_NAME}
    src/main.cpp
    ${IMGUI_SOURCES}
)

target_include_directories(${PROJECT_NAME} PRIVATE
    include
    external/imgui
    external/imgui/backends
    external/json/include
)

target_link_libraries(${PROJECT_NAME} PRIVATE
    OpenGL::GL
    glfw
    CURL::libcurl
    nlohmann_json::nlohmann_json
)
