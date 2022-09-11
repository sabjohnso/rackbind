cmake_minimum_required(VERSION 3.12)

project(rackbind VERSION 0.1.0 LANGUAGES C CXX)

option(rackbind_BUILD_TESTING "Build the rackbind tests" ON)
set(rackbind_CXX_STANDARD 20 CACHE STRING "C++ standard for rackbind")

include(GNUInstallDirs)
set(rackbind_INSTALL_BINDIR ${CMAKE_INSTALL_BINDIR})
set(rackbind_INSTALL_LIBDIR ${CMAKE_INSTALL_LIBDIR})
set(rackbind_INSTALL_INCLUDEDIR ${CMAKE_INSTALL_INCLUDEDIR})
set(rackbind_INSTALL_CONFDIR ${rackbind_INSTALL_LIBDIR}/cmake/rackbind-${PROJECT_VERSION})

list(INSERT CMAKE_MODULE_PATH 0 ${PROJECT_SOURCE_DIR}/cmake)
include(rackbind_deps)

add_subdirectory(rackbind)

if(rackbind_BUILD_TESTING)
  include(CTest)
  if(BUILD_TESTING)
    add_subdirectory(rackbind_testing)
  endif()
endif()

install(EXPORT rackbind_EXPORTS
  NAMESPACE rackbind::
  FILE rackbind-exports.cmake
  DESTINATION ${rackbind_INSTALL_CONFDIR})

configure_file(rackbind-config.cmake.in rackbind-config.cmake)
install(FILES ${PROJECT_BINARY_DIR}/rackbind-config.cmake
  DESTINATION ${rackbind_INSTALL_CONFDIR})
