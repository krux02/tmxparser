cmake_minimum_required(VERSION 2.8.3)
project(tmxparser)

set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}/cmake ${CMAKE_MODULE_PATH})

set(VERSION_MAJOR 1)
set(VERSION_MINOR 0)
set(VERSION_PATCH 0)

set(VERSION "${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_PATCH}")
message("Configuring tmxparser version ${VERSION}")

file(GLOB_RECURSE SOURCES 
    ${PROJECT_SOURCE_DIR}/src/*.cpp 
    ${PROJECT_SOURCE_DIR}/src/tinyxml/*.cpp
)

file(GLOB_RECURSE HEADERS 
    ${PROJECT_SOURCE_DIR}/src/*.h 
    ${PROJECT_SOURCE_DIR}/src/tinyxml/*.h
)

find_package(ZLIB)

set(LIB_CFLAGS "-pedantic -Werror -Wall -Werror=strict-prototypes -Werror=old-style-definition -Werror=missing-prototypes")
set(EXAMPLE_CFLAGS "-pedantic -Werror -Wall")


add_library(tmxparser_static STATIC ${SOURCES} ${HEADERS})
target_include_directories(tmxparser_static PUBLIC ${PROJECT_SOURCE_DIR}/src/tinyxml)

set_target_properties(tmxparser_static PROPERTIES
  OUTPUT_NAME tmxparser
  COMPILE_FLAGS ${LIB_CFLAGS})

add_library(tmxparser SHARED ${SOURCES} ${HEADERS})

target_include_directories(tmxparser PUBLIC ${PROJECT_SOURCE_DIR}/src/tinyxml)


set_target_properties(tmxparser PROPERTIES
  SOVERSION ${VERSION_MAJOR}
  VERSION ${VERSION}
  COMPILE_FLAGS ${LIB_CFLAGS})
target_link_libraries(tmxparser ${ZLIB_LIBRARIES})
include_directories(${ZLIB_INCLUDE_DIRS})

add_executable(test test/test.cpp)
set_target_properties(test PROPERTIES
  COMPILE_FLAGS ${EXAMPLE_CFLAGS})
target_link_libraries(test tmxparser)
install(FILES ${HEADERS} DESTINATION include/tmxparser)
install(TARGETS tmxparser tmxparser_static DESTINATION lib)
