add_library(sds sds.c ${sds_SOURCE_DIR}/include/sds.h ${sds_SOURCE_DIR}/include/sdsalloc.h)
set_target_properties(sds PROPERTIES POSITION_INDEPENDENT_CODE 1)
set_target_properties(sds PROPERTIES SOVERSION ${sds_SOVERSION})
add_library(sds::sds ALIAS sds)

target_include_directories(
  sds
  PUBLIC $<BUILD_INTERFACE:${sds_SOURCE_DIR}/include>
		 $<INSTALL_INTERFACE:include>)

if(MSVC)
  target_compile_options(sds PRIVATE $<$<CONFIG:RELEASE>:/Ox> /W4)
else()
  target_compile_options(sds PRIVATE $<$<CONFIG:RELEASE>:-O3> -Wall -Wextra
                                        -pedantic)
endif()

export(
  TARGETS ${sds_TARGET_NAME}
  NAMESPACE ${PROJECT_NAME}::
  FILE ${sds_CMAKE_PROJECT_TARGETS_FILE})
install(
  TARGETS ${sds_TARGET_NAME}
  EXPORT ${sds_TARGETS_EXPORT_NAME}
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
  INCLUDES DESTINATION ${sds_INCLUDE_INSTALL_DIR})