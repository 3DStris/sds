cmake_minimum_required(VERSION 3.12...3.15)

set(sds_SOVERSION 1)
set(sds_VERSION_MAJOR 1)
set(sds_VERSION_MINOR 0)
set(sds_VERSION_PATCH 0)

project(
  sds
  VERSION ${sds_VERSION_MAJOR}.${sds_VERSION_MINOR}.${sds_VERSION_PATCH}
  LANGUAGES C)

include(GNUInstallDirs)
set(sds_TARGET_NAME                ${PROJECT_NAME})
set(sds_CONFIG_INSTALL_DIR         "${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME}" CACHE INTERNAL "")
set(sds_INCLUDE_INSTALL_DIR        "${CMAKE_INSTALL_INCLUDEDIR}")
set(sds_TARGETS_EXPORT_NAME        "${PROJECT_NAME}Targets")
set(sds_CMAKE_CONFIG_TEMPLATE      "cmake/${PROJECT_NAME}Config.cmake.in")
set(sds_CMAKE_CONFIG_DIR           "${CMAKE_CURRENT_BINARY_DIR}")
set(sds_CMAKE_VERSION_CONFIG_FILE  "${sds_CMAKE_CONFIG_DIR}/${PROJECT_NAME}ConfigVersion.cmake")
set(sds_CMAKE_PROJECT_CONFIG_FILE  "${sds_CMAKE_CONFIG_DIR}/${PROJECT_NAME}Config.cmake")
set(sds_CMAKE_PROJECT_TARGETS_FILE "${sds_CMAKE_CONFIG_DIR}/${PROJECT_NAME}Targets.cmake")
set(sds_INCLUDE_BUILD_DIR		  "${PROJECT_SOURCE_DIR}/include/")

add_subdirectory(src)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  ${sds_CMAKE_VERSION_CONFIG_FILE}
  VERSION ${PACKAGE_VERSION}
  COMPATIBILITY SameMajorVersion)

configure_file(${sds_CMAKE_CONFIG_TEMPLATE}
               ${sds_CMAKE_PROJECT_CONFIG_FILE} @ONLY)
install(DIRECTORY ${sds_INCLUDE_BUILD_DIR}
        DESTINATION ${sds_INCLUDE_INSTALL_DIR})
install(
  FILES ${sds_CMAKE_PROJECT_CONFIG_FILE} ${sds_CMAKE_VERSION_CONFIG_FILE}		
  DESTINATION ${sds_CONFIG_INSTALL_DIR})

export(PACKAGE ${PROJECT_NAME})

install(
  EXPORT ${sds_TARGETS_EXPORT_NAME}
  NAMESPACE ${PROJECT_NAME}::
  DESTINATION ${sds_CONFIG_INSTALL_DIR})