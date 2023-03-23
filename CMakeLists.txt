cmake_minimum_required(VERSION 3.15)
project(yes VERSION 1.0 DESCRIPTION "A discord bot")

file(GLOB_RECURSE source_list "src/*.cpp" "src/*.hpp" "libs/imgui/imgui.cpp" "libs/imgui/imgui_demo.cpp" "libs/imgui/imgui_draw.cpp" "libs/imgui/imgui_tables.cpp" "libs/imgui/imgui_widgets.cpp" "libs/imgui/backends/imgui_impl_glfw.cpp" "libs/imgui/backends/imgui_impl_opengl3.cpp")
add_executable(${PROJECT_NAME} ${source_list})

target_include_directories(${PROJECT_NAME} PRIVATE "libs/imgui/" "libs/imgui/backends" "libs/glfw/include")

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_subdirectory(glfw)

target_link_libraries(${PROJECT_NAME}
    glfw
)
find_package(OpenGL REQUIRED)
target_link_libraries(${PROJECT_NAME} OpenGL::GL)

