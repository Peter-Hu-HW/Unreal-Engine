cmake_minimum_required(VERSION 3.0.0)
project(Lightflow VERSION 0.1.0)
set(CMAKE_CXX_STANDARD 17)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)
if(MSVC)
  add_definitions(/MP)
endif()



set(no_group_source_files
    "src/LightflowPCH.cpp"
    "src/LightflowPCH.h"
    "src/main.cpp"
)
source_group("" FILES ${no_group_source_files})

file(GLOB Framework "src/Framework/*.h" "src/Framework/*.cpp" "src/Framework/*/*.h" "src/Framework/*/*.cpp" )
source_group("Framework" FILES ${Framework})

set(Libs
    "libs/extensions_vk.cpp"
    "libs/extensions_vk.hpp"
    "libs/imgui/imconfig.h"
    "libs/imgui/imgui.cpp"
    "libs/imgui/imgui.h"
    "libs/imgui/imgui_demo.cpp"
    "libs/imgui/imgui_draw.cpp"
    "libs/imgui/imgui_impl_glfw.cpp"
    "libs/imgui/imgui_impl_glfw.h"
    "libs/imgui/imgui_impl_vulkan.cpp"
    "libs/imgui/imgui_impl_vulkan.h"
    "libs/imgui/imgui_internal.h"
    "libs/imgui/imgui_tables.cpp"
    "libs/imgui/imgui_widgets.cpp"
    "libs/imgui/imstb_rectpack.h"
    "libs/imgui/imstb_textedit.h"
    "libs/imgui/imstb_truetype.h"
    "libs/mitsuba_parser/tinyparser-mitsuba.cpp"
    "libs/tinyxml2/tinyxml2.cpp"
)
source_group("Libs" FILES ${Libs})

file(GLOB RayTracer
 "src/RayTracer/*.h"    "src/RayTracer/*.cpp" 
 "src/RayTracer/*/*.h"  "src/RayTracer/*/*.cpp" 
 "src/shaders/commons.h"
)
source_group("RayTracer" FILES ${RayTracer} )
 
set(ALL_FILES
    ${no_group_source_files}
    ${Framework}
    ${Libs}
    ${RayTracer}
)

################################################################################
# Target
################################################################################
message("PROJECT NAME is ${CMAKE_PROJECT_NAME}")
add_executable(${CMAKE_PROJECT_NAME} ${ALL_FILES})

if(MSVC)
target_precompile_headers(${CMAKE_PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src/LightflowPCH.h)
endif()

target_include_directories(${CMAKE_PROJECT_NAME} PUBLIC
"${CMAKE_CURRENT_SOURCE_DIR}/libs/glm;"
"${CMAKE_CURRENT_SOURCE_DIR}/libs/glfw/include;"
"${CMAKE_CURRENT_SOURCE_DIR}/libs/spdlog/include;"
"${CMAKE_CURRENT_SOURCE_DIR}/src;"
"${CMAKE_CURRENT_SOURCE_DIR}/libs/stb_image;"
"${CMAKE_CURRENT_SOURCE_DIR}/libs/gli;"
"${CMAKE_CURRENT_SOURCE_DIR}/libs/tinygltf;"
"${CMAKE_CURRENT_SOURCE_DIR}/libs/imgui;"
"${CMAKE_CURRENT_SOURCE_DIR}/libs"
)

################################################################################
# Dependencies
################################################################################

## GLFW3
add_subdirectory(libs/glfw EXCLUDE_FROM_ALL)
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE glfw)

## VULKAN
find_package(Vulkan REQUIRED)
target_link_libraries( ${CMAKE_PROJECT_NAME} PUBLIC Vulkan::Vulkan)

# PYTHON
set(LINK_WITH_PYTHON False)


if(${LINK_WITH_PYTHON})
    find_package(PythonLibs REQUIRED)
    include_directories(${PYTHON_INCLUDE_DIRS})
    target_link_libraries(${CMAKE_PROJECT_NAME} PUBLIC ${PYTHON_LIBRARIES})
    target_compile_options(${CMAKE_PROJECT_NAME} PRIVATE -DLINK_WITH_PYTHON)
endif()

if(MSVC) 
    target_link_options(${CMAKE_PROJECT_NAME} PUBLIC /INCREMENTAL)
endif()

## Enable compiler warnings.
if(MSVC)
  target_compile_options(${CMAKE_PROJECT_NAME} PRIVATE /W4 /WX)
else()
#   target_compile_options(${CMAKE_PROJECT_NAME} PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif()