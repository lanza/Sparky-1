cmake_minimum_required(VERSION 3.17)

set(CMAKE_CXX_STANDARD 20 CACHE STRING "" FORCE)

set(CMAKE_CXX_COMPILER /Users/lanza/.llvm/bin/clang++)

project("Sparky" CXX C)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

add_compile_options(-fcolor-diagnostics)

set(LLVM_DIR ~/.llvm/lib/cmake/llvm)
find_package(LLVM REQUIRED)
include_directories(${LLVM_INCLUDE_DIRS})
find_package(ZLIB REQUIRED)
find_package(OpenGL REQUIRED)

if(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
  add_compile_definitions(GL_SILENCE_DEPRECATION)
endif()


include_directories(include)

add_subdirectory(utils)

add_executable(
  sparky
  Sparky-core/src/graphics/buffers/buffer.cpp
  Sparky-core/src/graphics/buffers/indexbuffer.cpp
  Sparky-core/src/graphics/buffers/vertexarray.cpp
  Sparky-core/src/graphics/BatchRenderer2D.cpp
  Sparky-core/src/graphics/simple2drenderer.cpp
  Sparky-core/src/graphics/static_sprite.cpp
  Sparky-core/src/graphics/sprite.cpp
  Sparky-core/src/graphics/shader.cpp
  Sparky-core/src/graphics/window.cpp
  Sparky-core/src/maths/mat4.cpp
  Sparky-core/src/maths/vec2.cpp
  Sparky-core/src/maths/vec3.cpp
  Sparky-core/src/maths/vec4.cpp
  Sparky-core/main.cpp
)

target_link_libraries(
  sparky
  libglew_shared
  glfw
  OpenGL::GL
)
