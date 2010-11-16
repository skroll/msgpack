cmake_minimum_required(VERSION 2.6)
project(msgpack)

set (VERSION "0.5.4")
set (VERSION_MAJOR 0)
set (VERSION_MINOR 5)

configure_file(
	"${PROJECT_SOURCE_DIR}/src/msgpack/version.h.in"
	"${PROJECT_BINARY_DIR}/msgpack/version.h"
)

include_directories(${PROJECT_BINARY_DIR}
                    ${PROJECT_SOURCE_DIR}/src)

set(C_SOURCES
	${PROJECT_SOURCE_DIR}/src/objectc.c
	${PROJECT_SOURCE_DIR}/src/unpack.c
	${PROJECT_SOURCE_DIR}/src/version.c
	${PROJECT_SOURCE_DIR}/src/vrefbuffer.c
	${PROJECT_SOURCE_DIR}/src/zone.c)

set(C_HEADERS
	${PROJECT_SOURCE_DIR}/src/msgpack.h)

set(C_HEADERS_MSGPACK
	${PROJECT_SOURCE_DIR}/src/msgpack/object.h
	${PROJECT_SOURCE_DIR}/src/msgpack/pack.h
	${PROJECT_SOURCE_DIR}/src/msgpack/pack_define.h
	${PROJECT_SOURCE_DIR}/src/msgpack/pack_template.h
	${PROJECT_SOURCE_DIR}/src/msgpack/sbuffer.h
	${PROJECT_SOURCE_DIR}/src/msgpack/sysdep.h
	${PROJECT_SOURCE_DIR}/src/msgpack/unpack.h
	${PROJECT_SOURCE_DIR}/src/msgpack/unpack_define.h
	${PROJECT_SOURCE_DIR}/src/msgpack/unpack_template.h
	${PROJECT_SOURCE_DIR}/src/msgpack/vrefbuffer.h
	${PROJECT_SOURCE_DIR}/src/msgpack/zbuffer.h
	${PROJECT_SOURCE_DIR}/src/msgpack/zone.h
	${PROJECT_BINARY_DIR}/msgpack/version.h)

set(CPP_SOURCES
	${PROJECT_SOURCE_DIR}/src/object.cpp)

set(CPP_HEADERS
	${PROJECT_SOURCE_DIR}/src/msgpack.hpp)

set(CPP_HEADERS_MSGPACK
	${PROJECT_SOURCE_DIR}/src/msgpack/object.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/pack.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/sbuffer.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/unpack.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/vrefbuffer.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/zbuffer.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/zone.hpp)

set(CPP_HEADERS_TYPES
	${PROJECT_SOURCE_DIR}/src/msgpack/types/bool.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/define.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/deque.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/fixint.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/float.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/int.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/list.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/map.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/nil.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/pair.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/raw.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/set.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/string.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/tuple.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/vector.hpp)

set(CPP_HEADERS_TR1
	${PROJECT_SOURCE_DIR}/src/msgpack/types/tr1/unordered_map.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/types/tr1/unordered_set.hpp)

add_library(msgpack
	${C_SOURCES}
	${C_HEADERS}
	${C_HEADERS_MSGPACK})

install(
	TARGETS msgpack
	DESTINATION lib
)

install(
	FILES ${C_HEADERS}
	DESTINATION include
)

install(
	FILES ${C_HEADERS_MSGPACK}
	DESTINATION include/msgpack
)
