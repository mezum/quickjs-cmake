# Copyright (c) 2020 Kosaki Mezumona
# This cmake script is distributed under the MIT License.
# See LICENSE for more details.
cmake_minimum_required(VERSION 3.1)
project(quickjs)

set(quickjs_version 2020-01-05)
set(quickjs_url https://bellard.org/quickjs/quickjs-${quickjs_version}.tar.xz)
set(quickjs_sha1 5f6d100e7614ee8ee1d89dd51f902f4ab84bf892)
set(quickjs_extras_url https://bellard.org/quickjs/quickjs-extras-${quickjs_version}.tar.xz)
set(quickjs_extras_sha1 33df8073eca9a6be53584d835744bd9eac98f621)
set(quickjs_extract_dir ${CMAKE_CURRENT_BINARY_DIR}/sources)
set(quickjs_sources_root ${quickjs_extract_dir}/quickjs-${quickjs_version})
set(quickjs_sources
	${quickjs_sources_root}/quickjs.h
	${quickjs_sources_root}/quickjs-libc.h
	${quickjs_sources_root}/quickjs.c
	${quickjs_sources_root}/libregexp.c
	${quickjs_sources_root}/libunicode.c
	${quickjs_sources_root}/libbf.c
	${quickjs_sources_root}/cutils.c
	${quickjs_sources_root}/quickjs-libc.c
)

set(get_quickjs_cmake_in ${CMAKE_CURRENT_LIST_DIR}/get_quickjs.cmake.in)
set(get_quickjs_cmake ${CMAKE_CURRENT_BINARY_DIR}/get_quickjs.cmake)
configure_file(
	${get_quickjs_cmake_in}
	${get_quickjs_cmake}
	@ONLY
)
add_custom_command(
	OUTPUT
		${quickjs_sources}
	DEPENDS
		${get_quickjs_cmake}
	COMMENT
		Get quickjs sources.
	COMMAND ${CMAKE_COMMAND} -P ${CMAKE_CURRENT_BINARY_DIR}/get_quickjs.cmake
)

add_library(${PROJECT_NAME}
	${quickjs_sources}
)
target_compile_definitions(${PROJECT_NAME}
	PRIVATE
		CONFIG_VERSION="${quickjs_version}"
)
target_include_directories(${PROJECT_NAME}
	PUBLIC
		${quickjs_sources_root}
)
