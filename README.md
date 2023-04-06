# ED_SLAacc
SLA of PFT change with CO2 concentration

**11 files have been changed in this ED version**
- init/ed_params.f90 ok
- memory/pft_coms.f90 ok
- memory/ename_coms.f90 ok
- dynamics/structural_growth.f90
- dynamics/reproduction.f90
- utils/update_derived_utils.f90
- io/ed_read_ed21_history.f90
- io/ed_read_ed10_20_history.f90
- io/ed_load_namelist.f90 ok
- io/ed_xml_config.f90 ok
- io/ed_opspec.F90 ok

## note
If allowing SLA to change with CO2, NL%TRAIT_PLASTICITY_SCHEME **NOT** equal to 0, NL%ISTRUCT_GROWTH_SCHEME **MUST** euqal to 2

## The specifc modifications:
1. adding a new parameter: kplastic_ref_lai
- This paramter is for trait_plasticity_scheme=3, and used to determine kplastic_vm0, kplastic_LL. The equations are derived from observation in BCI.
- This parameter can be set through xml
- refers to "init/ed_params.f90", "memory/pft_coms.f90" and "io/ed_xml_config.f90"
2. adding a new input variable: NL%include_these_pft_sla
- This paramter is used to specify SLA of which pfts can change with CO2 
- The input form is like "NL%include_these_pft"
- refers to " "init/ed_params.f90", "memory/pft_coms.f90", "memory/ename_coms.f90" and "io/ed_load_namelist.f90"
3. adding a new option for struct growth scheme, i.e., ISTRUCT_GROWTH_SCHEME=2
- ISTRUCT_GROWTH_SCHEME must be set to 2 if allowing SLA to be plastic, i.e., NL%TRAIT_PLASTICITY_SCHEME not equal to 0
- This option determine "f_bdeada", "f_bdeadb" according to current biomass fraction of dead tissue.
- refers to "dynamics/structural_growth.f90" and "io/ed_opspec.F90"
4. SLA change with CO2
- SLA change with CO2 concentration at monthly or yearly scale, which depends on NL%TRAIT_PLASTICITY_SCHEME. The equation is from (Poorter et al. 2022)[^1]
- mainly refers to "utils/update_derived_utils.f90"
- also refers to "dynamics/structural_growth.f90","dynamics/reproduction.f90", "io/ed_read_ed21_history.f90", "io/ed_read_ed10_20_history.f90" where "update_derived_utils" is called. 

[^1]: Poorter, H. et al. A meta-analysis of responses of C3 plants to atmospheric CO2: dose–response curves for 85 traits ranging from the molecular to the whole-plant level. New Phytologist 233, 1560–1596 (2022).

