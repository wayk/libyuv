
cmake_minimum_required(VERSION 2.8)

project(YUV C CXX)

set(MODULE_NAME "yuv")
set(MODULE_PREFIX "LIBYUV")

if(WIN32)
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /W3")
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -D_CRT_SECURE_NO_WARNINGS")
	set(variables CMAKE_C_FLAGS CMAKE_C_FLAGS_DEBUG CMAKE_C_FLAGS_RELEASE)
	foreach(variable ${variables})
		if(${variable} MATCHES "/MD") # force MSVC static runtime
			string(REGEX REPLACE "/MD" "/MT" ${variable} "${${variable}}")
		endif()
	endforeach()
endif()

set(${MODULE_PREFIX}_HEADERS "")

set(${MODULE_PREFIX}_SOURCES
	source/compare.cc
	source/compare_common.cc
	source/compare_gcc.cc
	source/compare_neon.cc
	source/compare_neon64.cc
	source/compare_win.cc
	source/convert.cc
	source/convert_argb.cc
	source/convert_from.cc
	source/convert_from_argb.cc
	source/convert_to_argb.cc
	source/convert_to_i420.cc
	source/cpu_id.cc
	source/planar_functions.cc
	source/rotate.cc
	source/rotate_any.cc
	source/rotate_argb.cc
	source/rotate_common.cc
	source/rotate_dspr2.cc
	source/rotate_gcc.cc
	source/rotate_msa.cc
	source/rotate_neon.cc
	source/rotate_neon64.cc
	source/rotate_win.cc
	source/row_any.cc
	source/row_common.cc
	source/row_dspr2.cc
	source/row_gcc.cc
	source/row_msa.cc
	source/row_neon.cc
	source/row_neon64.cc
	source/row_win.cc
	source/scale.cc
	source/scale_any.cc
	source/scale_argb.cc
	source/scale_common.cc
	source/scale_dspr2.cc
	source/scale_gcc.cc
	source/scale_msa.cc
	source/scale_neon.cc
	source/scale_neon64.cc
	source/scale_win.cc
	source/video_common.cc)

set_source_files_properties(${${MODULE_PREFIX}_SOURCES} PROPERTIES LANGUAGE C)

set(${MODULE_PREFIX}_JPEG_SOURCES
	source/convert_jpeg.cc
	source/mjpeg_decoder.cc
	source/mjpeg_validate.cc)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

add_library(${MODULE_NAME} STATIC ${${MODULE_PREFIX}_SOURCES})
set_target_properties(${MODULE_NAME} PROPERTIES PREFIX "lib")

