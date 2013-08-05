add_executable(gnucap-ui main.cc)

target_link_libraries(gnucap-ui gnucap gnucap-default-plugins)

install(PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/gnucap-ui
    DESTINATION ${CMAKE_INSTALL_BINDIR} RENAME gnucap)
