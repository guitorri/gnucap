add_executable(gnucap-ui main.cc)
set_target_properties(gnucap-ui PROPERTIES OUTPUT_NAME "gnucap")

target_link_libraries(gnucap-ui gnucap)

install(TARGETS gnucap-ui RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})
