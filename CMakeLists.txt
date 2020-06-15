cmake_minimum_required(VERSION 3.16)
project(tutorial C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_VERBOSE_MAKEFILE ON)

find_package(PkgConfig REQUIRED)

pkg_check_modules(avformat REQUIRED libavformat IMPORTED_TARGET)
pkg_check_modules(avcodec REQUIRED libavcodec IMPORTED_TARGET)
pkg_check_modules(avutil REQUIRED libavutil IMPORTED_TARGET)
pkg_check_modules(swscale REQUIRED libswscale IMPORTED_TARGET)
set(Ffmpeg_LIBS
  PkgConfig::avformat
  PkgConfig::avcodec
  PkgConfig::avutil
  PkgConfig::swscale)
message(STATUS "Ffmpeg imported targets: ${Ffmpeg_LIBS}")

add_executable(hello_world 0_hello_world.c)
target_link_libraries(hello_world ${Ffmpeg_LIBS})

add_executable(remuxing 2_remuxing.c)
target_link_libraries(remuxing ${Ffmpeg_LIBS})

add_executable(transcoding 3_transcoding.c)
target_link_libraries(transcoding ${Ffmpeg_LIBS})