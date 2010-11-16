cmake_minimum_required(VERSION 2.6)
project(msgpack)

set(VERSION "0.5.4")
set(VERSION_MAJOR 0)
set(VERSION_MINOR 5)

configure_file(
	"${PROJECT_SOURCE_DIR}/src/msgpack/version.h.in"
	"${PROJECT_BINARY_DIR}/msgpack/version.h"
)

make_directory(${PROJECT_BINARY_DIR}/msgpack)
make_directory(${PROJECT_BINARY_DIR}/msgpack/type)

find_package(Ruby REQUIRED)

foreach(HDR "zone.hpp" "type/define.hpp" "type/tuple.hpp")
	execute_process(
		COMMAND ${RUBY_EXECUTABLE} -r erb -e "puts ERB.new(ARGF.read).result" ${PROJECT_SOURCE_DIR}/src/msgpack/${HDR}.erb
		OUTPUT_FILE ${PROJECT_BINARY_DIR}/msgpack/${HDR}
	)
endforeach(HDR)
	
include_directories(
	${PROJECT_BINARY_DIR}
	${PROJECT_BINARY_DIR}/msgpack
	${PROJECT_SOURCE_DIR}/src
	${PROJECT_SOURCE_DIR}/src/msgpack
	${PROJECT_SOURCE_DIR}/..
	${PROJECT_SOURCE_DIR}/../msgpack
)

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
	${PROJECT_SOURCE_DIR}/src/msgpack/sbuffer.h
	${PROJECT_SOURCE_DIR}/src/msgpack/unpack.h
	${PROJECT_SOURCE_DIR}/src/msgpack/vrefbuffer.h
	${PROJECT_SOURCE_DIR}/src/msgpack/zbuffer.h
	${PROJECT_SOURCE_DIR}/src/msgpack/zone.h
	${PROJECT_SOURCE_DIR}/../msgpack/pack_define.h
	${PROJECT_SOURCE_DIR}/../msgpack/pack_template.h
	${PROJECT_SOURCE_DIR}/../msgpack/sysdep.h
	${PROJECT_SOURCE_DIR}/../msgpack/unpack_define.h
	${PROJECT_SOURCE_DIR}/../msgpack/unpack_template.h
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
	${PROJECT_BINARY_DIR}/msgpack/zone.hpp)

set(CPP_HEADERS_TYPES
	${PROJECT_SOURCE_DIR}/src/msgpack/type/bool.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/deque.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/fixint.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/float.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/int.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/list.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/map.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/nil.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/pair.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/raw.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/set.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/string.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/vector.hpp
	${PROJECT_BINARY_DIR}/msgpack/type/define.hpp
	${PROJECT_BINARY_DIR}/msgpack/type/tuple.hpp)

set(CPP_HEADERS_TR1
	${PROJECT_SOURCE_DIR}/src/msgpack/type/tr1/unordered_map.hpp
	${PROJECT_SOURCE_DIR}/src/msgpack/type/tr1/unordered_set.hpp)

add_library(msgpack
	${C_SOURCES}
	${C_HEADERS}
	${C_HEADERS_MSGPACK}
	${CPP_SOURCES}
	${CPP_HEADERS}
	${CPP_HEADERS_MSGPACK}
	${CPP_HEADERS_TYPES}
	${CPP_HEADERS_TR1}
)

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
