

cmake_minimum_required(VERSION 3.16)

project(HelloWorld LANGUAGES CXX)


set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_CXX_STANDARD 20)

if(MSVC)
    add_compile_options(
        $<$<CONFIG:>:/MT> 
        $<$<CONFIG:Debug>:/MTd>
        $<$<CONFIG:Release>:/MT>
    )
endif()

include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()


set(target helloworld)

add_executable( ${target} 
${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp 
${CMAKE_CURRENT_SOURCE_DIR}/bindings/imgui_impl_glfw.cpp 
${CMAKE_CURRENT_SOURCE_DIR}/bindings/imgui_impl_opengl3.cpp 
)
target_include_directories(${target} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/bindings)
target_compile_definitions(${target} PUBLIC IMGUI_IMPL_OPENGL_LOADER_GLEW)

target_link_libraries(${target} ${CONAN_LIBS})

