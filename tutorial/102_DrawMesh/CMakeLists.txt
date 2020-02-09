get_filename_component(PROJECT_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)
project(${PROJECT_NAME})

add_executable(${PROJECT_NAME}_bin main.cpp)
target_link_libraries(${PROJECT_NAME}_bin igl::core igl::opengl igl::opengl_glfw tutorials)

if (EMSCRIPTEN)
  set_target_properties(${PROJECT_NAME}_bin PROPERTIES
    COMPILE_FLAGS "-s USE_GLFW=3"
    LINK_FLAGS "-s USE_GLFW=3 -s USE_WEBGL2=1 --embed-file ${TUTORIAL_SHARED_PATH}/bunny.off@bunny.off --emrun"
    SUFFIX ".html")
endif()
