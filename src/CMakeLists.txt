include_directories("${PROJECT_SOURCE_DIR}")

set(SOURCE_FILES
    bsd_rand.c
    glsl_shader_source.cpp
    image_png.cpp
    intro.cpp
    main.cpp
    dnload.h)

if (APPLE)
    list(APPEND SOURCE_FILES SDLMain.mm)
    add_executable(junamatkailuintro MACOSX_BUNDLE ${SOURCE_FILES})
else (APPLE)
    add_executable(junamatkailuintro ${SOURCE_FILES})
endif (APPLE)


add_custom_command(
    OUTPUT dnload.h
    DEPENDS intro.cpp
    COMMAND sh refresh.sh
    WORKING_DIRECTORY ..)

target_link_libraries(junamatkailuintro ${BOOST_PROGRAM_OPTIONS_LIBRARY})
target_link_libraries(junamatkailuintro ${PNG_LIBRARY})
target_link_libraries(junamatkailuintro ${SDL_LIBRARY})
if(RASPBERRY_PI_FOUND)
  target_link_libraries(junamatkailuintro ${BCM_HOST_LIBRARY})
  target_link_libraries(junamatkailuintro ${EGL_LIBRARY})
  target_link_libraries(junamatkailuintro ${OPENGL_gl_LIBRARY})
else()
  target_link_libraries(junamatkailuintro ${OPENGL_gl_LIBRARY})
  target_link_libraries(junamatkailuintro ${GLEW_LIBRARY})
endif()
