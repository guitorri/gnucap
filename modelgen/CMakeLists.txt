add_executable(gnucap-modelgen
    mg_error.cc
    mg_in.cc
    mg_main.cc
    mg_out_common.cc
    mg_out_dev.cc
    mg_out_dump.cc
    mg_out_h.cc
    mg_out_lib.cc
    mg_out_model.cc
    mg_out_root.cc
)

target_link_libraries(gnucap-modelgen gnucap)

install(TARGETS gnucap-modelgen DESTINATION ${CMAKE_INSTALL_BINDIR})
