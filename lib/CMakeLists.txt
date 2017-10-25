add_library(gnucap SHARED
    globals.cc
    ap_construct.cc
    ap_convert.cc
    ap_error.cc
    ap_get.cc
    ap_match.cc
    ap_skip.cc
    bm.cc
    bm_cond.cc
    bm_value.cc
    c__cmd.cc
    c_attach.cc
    c_file.cc
    d_logic.cc
    d_logicmod.cc
    d_subckt.cc
    e_base.cc
    e_card.cc
    e_cardlist.cc
    e_paramlist.cc
    e_ccsrc.cc
    e_compon.cc
    e_elemnt.cc
    e_model.cc
    e_node.cc
    e_storag.cc
    findbr.cc
    io.cc
    io_contr.cc
    io_error.cc
    io_findf.cc
    io_out.cc
    io_xopen.cc
    l_ftos.cc
    l_pmatch.cc
    l_timer.cc
    l_trim.cc
    l_wmatch.cc
    m_base_in.cc
    m_base_math.cc
    m_expression_dump.cc
    m_expression_in.cc
    m_expression_reduce.cc
    m_fft.cc
    m_spline.cc
    plot.cc
    u_lang.cc
    u_nodemap.cc
    u_opt1.cc
    u_opt2.cc
    u_parameter.cc
    u_prblst.cc
    u_probe.cc
    u_sim_data.cc
    u_xprobe.cc
)

target_link_libraries(gnucap ${DL_LIBRARIES} ${READLINE_LIBS})

set_target_properties(gnucap PROPERTIES INSTALL_NAME_DIR ${CMAKE_INSTALL_FULL_LIBDIR})

install(TARGETS gnucap DESTINATION ${CMAKE_INSTALL_LIBDIR})
