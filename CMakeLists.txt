project(sds C)

add_library(sds STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sds.h ${CMAKE_CURRENT_SOURCE_DIR}/sds.c ${CMAKE_CURRENT_SOURCE_DIR}/sdsalloc.h)
target_include_directories(sds PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
