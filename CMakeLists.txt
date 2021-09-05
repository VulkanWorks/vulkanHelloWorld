cmake_minimum_required (VERSION 3.10)
project (vulkanHelloWorld)

add_executable(${PROJECT_NAME} main.cpp)
set_property(TARGET vulkanHelloWorld PROPERTY CXX_STANDARD 17)

find_package(Vulkan REQUIRED)
include_directories(${Vulkan_INCLUDE_DIRS})
find_library(SHADERC_LIB shaderc_combined $ENV{VULKAN_SDK}/lib)
MESSAGE(STATUS "Found shaderc in: ${SHADERC_LIB}")

# setup GLFW
add_subdirectory("${PROJECT_SOURCE_DIR}/third_party/glfw")
include_directories("${PROJECT_SOURCE_DIR}/third_party/glfw/include/GLFW")

# add libraries (note that as of version 3.7, CMake supports Vulkan out-of-the-box)
target_link_libraries(${PROJECT_NAME} glfw ${GLFW_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${Vulkan_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${SHADERC_LIB})
