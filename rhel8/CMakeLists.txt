# Sometimes our users will try to do: "cd rhel8; cmake ." That needs to error in a nice way.
if ("${CMAKE_SOURCE_DIR}" STREQUAL "${CMAKE_CURRENT_SOURCE_DIR}")
    message(FATAL_ERROR "cmake has to be used on the root CMakeLists.txt, see the developer_guide.adoc for more details!")
endif()

set(PRODUCT "rhel8")
set(DISA_SRG_TYPE "os")

ssg_build_product(${PRODUCT})

ssg_build_html_table_by_ref(${PRODUCT} "nist")
ssg_build_html_table_by_ref(${PRODUCT} "cui")
ssg_build_html_table_by_ref(${PRODUCT} "cis")
ssg_build_html_table_by_ref(${PRODUCT} "pcidss")
ssg_build_html_table_by_ref(${PRODUCT} "anssi")

ssg_build_html_nistrefs_table(${PRODUCT} "standard")
ssg_build_html_nistrefs_table(${PRODUCT} "ospp")

# Uncomment when anssi profiles are marked documentation_complete: true
#ssg_build_html_anssirefs_table(${PRODUCT} "nt28_minimal")
#ssg_build_html_anssirefs_table(${PRODUCT} "nt28_intermediary")
#ssg_build_html_anssirefs_table(${PRODUCT} "nt28_enhanced")
#ssg_build_html_anssirefs_table(${PRODUCT} "nt28_high")

ssg_build_html_cce_table(${PRODUCT})

ssg_build_html_srgmap_tables(${PRODUCT} ${DISA_SRG_TYPE})

#ssg_build_html_stig_tables(${PRODUCT} "ospp")

if (SSG_CENTOS_DERIVATIVES_ENABLED)
    ssg_build_derivative_product(${PRODUCT} "centos" "centos8")
endif()
