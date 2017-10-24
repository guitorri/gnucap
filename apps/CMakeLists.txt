function(add_models output_var)
    set(result)

    foreach(model ${ARGN})
        get_filename_component(model_name ${model} NAME_WE)

        set(model_source ${CMAKE_CURRENT_SOURCE_DIR}/${model})
        set(model_out ${CMAKE_CURRENT_BINARY_DIR}/${model_name}.cc)

        add_custom_command(
            OUTPUT ${model_out}
            COMMAND gnucap-modelgen ${model_source}
            DEPENDS gnucap-modelgen ${model_source}
        )

        list(APPEND result "${model_out}")
    endforeach()

    set(${output_var} "${result}" PARENT_SCOPE)
endfunction()

set(MODELS
    d_mos1.model d_mos2.model d_mos3.model
    d_mos4.model d_mos5.model d_mos6.model d_mos7.model d_mos8.model
    d_mos123.model d_mos_base.model d_mos.model
    d_bjt.model d_diode.model
)

set(D_SRCS
    d_admit.cc d_cap.cc d_cccs.cc d_ccvs.cc d_coil.cc
    d_cs.cc d_poly_g.cc d_poly_cap.cc d_res.cc d_switch.cc
    d_trln.cc d_vcg.cc d_vcr.cc d_vcvs.cc d_vs.cc
    d_meter.cc
)

set(BM_SRCS
    bm_complex.cc bm_exp.cc bm_fit.cc bm_generator.cc
    bm_model.cc bm_poly.cc bm_posy.cc bm_pulse.cc bm_pwl.cc bm_sffm.cc
    bm_sin.cc bm_tanh.cc bmm_table.cc bmm_semi.cc
)

set(C_SRCS
    c_clear.cc c_comand.cc c_delete.cc c_exp.cc  c_genrat.cc
    c_list.cc c_measure.cc c_modify.cc c_param.cc c_prbcmd.cc
    c_status.cc c_sweep.cc c_sim.cc c_system.cc
)

set(S_SRCS
    s__init.cc s__out.cc s__solve.cc
    s_ac.cc s_dc.cc s_fo.cc
    s_tr.cc s_tr_set.cc s_tr_swp.cc
)

set(LANG_SRCS
    lang_spice.cc lang_spectre.cc lang_verilog.cc
)

set(FUNC_SRCS
    func_core.cc measure_eval.cc
    measure_max.cc measure_min.cc measure_slewrate.cc measure_cross.cc
    measure_integral.cc measure_average.cc measure_rms.cc measure_at.cc
)

set(OTHER_SOURCES
    signon.cc
)

add_models(MODEL_SOURCES ${MODELS})

add_library(gnucap-default-plugins MODULE
    ${D_SRCS}
    ${BM_SRCS}
    ${C_SRCS}
    ${S_SRCS}
    ${LANG_SRCS}
    ${FUNC_SRCS}
    ${OTHER_SOURCES}
    ${MODEL_SOURCES}
)

if(APPLE)
  set(CMAKE_MODULE_LINKER_FLAGS "-undefined dynamic_lookup")
endif()

install(TARGETS gnucap-default-plugins
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/gnucap")
