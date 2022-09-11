configure_file(config.hpp.in config.hpp)

add_library(rackbind_header INTERFACE)
set_target_properties(rackbind_header PROPERTIES EXPORT_NAME header)
target_include_directories(rackbind_header
  INTERFACE
  $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}>
  $<BUILD_INTERFACE:${PROJECT_BINARY_DIR}>
  $<INSTALL_INTERFACE:${rackbind_INSTALL_INCLUDEDIR}>)

add_library(rackbind::header ALIAS rackbind_header)
  
install(TARGETS rackbind_header
  EXPORT rackbind_EXPORTS
  RUNTIME DESTINATION ${rackbind_INSTALL_BINDIR}
  LIBRARY DESTINATION ${rackbind_INSTALL_LIBDIR}
  ARCHIVE DESTINATION ${rackbind_INSTALL_LIBDIR})

install(FILES
  ${CMAKE_CURRENT_BINARY_DIR}/config.hpp
  DESTINATION ${rackbind_INSTALL_INCLUDEDIR}/rackbind)
