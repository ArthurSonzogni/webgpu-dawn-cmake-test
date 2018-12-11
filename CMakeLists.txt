cmake_minimum_required(VERSION 3.11)
project(test)

add_definitions(-DDAWN_ENABLE_BACKEND_VULKAN)
#add_definitions(-DDAWN_ENABLE_BACKEND_OPENGL)

# glfw
set(GLFW_BUILD_EXAMPLES OFF CACHE STRING "" FORCE)
set(GLFW_BUILD_TESTS    OFF CACHE STRING "" FORCE)
set(GLFW_INSTALL        OFF CACHE STRING "" FORCE)
add_subdirectory(./third_party/glfw)
include_directories(./third_party/glfw/include)

# glad
add_subdirectory(./third_party/glad)

# glslang
add_subdirectory(./third_party/glslang)

# SPIRV-Headers
add_subdirectory(./third_party/SPIRV-Headers)

# SPIRV-Tools
add_subdirectory(./third_party/SPIRV-Tools)

# shaderc
set(SHADERC_SKIP_INSTALL ON CACHE STRING "" FORCE)
set(SHADERC_SKIP_TESTS ON CACHE STRING "" FORCE)
add_subdirectory(./third_party/shaderc)

# Vulkan
find_package(Vulkan REQUIRED)

add_executable(Test
  src/main.cpp
  src/SampleUtils.cpp
  src/utils/BackendBinding.cpp
  src/utils/BackendBinding.h
  #src/utils/D3D12Binding.cpp
  src/utils/DawnHelpers.cpp
  src/utils/DawnHelpers.h
  #src/utils/MetalBinding.mm
  #src/utils/NullBinding.cpp
  #src/utils/OpenGLBinding.cpp
  src/utils/SystemUtils.cpp
  src/utils/SystemUtils.h
  src/utils/TerribleCommandBuffer.cpp
  src/utils/TerribleCommandBuffer.h
  src/utils/VulkanBinding.cpp
)

target_link_libraries(Test
  PRIVATE /home/sonzogna/programmation/download/dawn/out/Release/libdawn.so
  PRIVATE /home/sonzogna/programmation/download/dawn/out/Release/libdawn_common.so
  PRIVATE /home/sonzogna/programmation/download/dawn/out/Release/libdawn_native.so
  PRIVATE /home/sonzogna/programmation/download/dawn/out/Release/libdawn_wire.so
  PRIVATE /home/sonzogna/programmation/download/dawn/out/Release/libc++.so
  PRIVATE Vulkan::Vulkan
  PRIVATE glad
  PRIVATE glfw
  PRIVATE shaderc
  PRIVATE Vulkan::Vulkan
)

target_include_directories(Test
  PRIVATE ./src/
  PRIVATE /home/sonzogna/programmation/download/dawn/include/
  PRIVATE /home/sonzogna/programmation/download/dawn/out/Release/gen/
  PRIVATE /home/sonzogna/programmation/download/dawn/src/
  PRIVATE /home/sonzogna/programmation/download/dawn/src/include/
)
