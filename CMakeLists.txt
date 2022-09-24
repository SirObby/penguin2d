cmake_minimum_required(VERSION 3.15)

project(penguin2d VERSION 1.0 DESCRIPTION "A 2D Game engine")

find_package(OpenGL)

# GLFW
set(GLFW_DIR ./libs/glfw) # Set this to point to an up-to-date GLFW repo
option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" OFF)
option(GLFW_BUILD_TESTS "Build the GLFW test programs" OFF)
option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_INSTALL "Generate installation target" OFF)
option(GLFW_DOCUMENT_INTERNALS "Include internals in documentation" OFF)
add_subdirectory(${GLFW_DIR} binary_dir EXCLUDE_FROM_ALL)
include_directories(${GLFW_DIR}/include)

# Dear ImGui
set(IMGUI_DIR ./libs/imgui)
include_directories(${IMGUI_DIR} ${IMGUI_DIR}/backends ..)
file(GLOB imgui_sources ${IMGUI_DIR}/backends/imgui_impl_glfw.cpp ${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp ${IMGUI_DIR}/imgui.cpp ${IMGUI_DIR}/imgui_draw.cpp ${IMGUI_DIR}/imgui_demo.cpp ${IMGUI_DIR}/imgui_tables.cpp ${IMGUI_DIR}/imgui_widgets.cpp)

file(GLOB_RECURSE source_list "src/*.cpp" "src/*/*.cpp")

add_executable(${PROJECT_NAME} ${source_list} ${imgui_sources})

target_link_libraries(penguin2d glfw;OpenGL::GL)
