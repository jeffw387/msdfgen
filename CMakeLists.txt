cmake_minimum_required(VERSION 2.8.12)

project(msdfgen)

# Make release mode default (turn on optimizations)
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()


# Note: Clang doesn't support openMP by default...
#find_package(OpenMP)
#if (OPENMP_FOUND)
#	set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
#	set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
#endif()

file(GLOB_RECURSE msdfgen_HEADERS
  "core/*.h"
	# "lib/*.h"
	# "ext/*.h"
	# "include/*.h"
)
list(APPEND msdfgen_HEADERS msdfgen.h)

file(GLOB_RECURSE msdfgen_SOURCES
	"core/*.cpp"
	# "lib/*.cpp"
	# "ext/*.cpp"
)

add_library(lib_msdfgen ${msdfgen_SOURCES} ${msdfgen_HEADERS})
target_include_directories(lib_msdfgen PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
set_target_properties(lib_msdfgen PROPERTIES OUTPUT_NAME msdfgen)
target_compile_definitions(lib_msdfgen PRIVATE -DMSDFGEN_USE_CPP11)
