cmake_minimum_required(VERSION 2.8)

set(PROJECT jpeg)

project(${PROJECT} C)

# file(GLOB HEADERS include/*.h)
# aux_source_directory(src SOURCES)

# source files: JPEG library proper
set(LIBSOURCES
        jaricom.c jcapimin.c jcapistd.c jcarith.c jccoefct.c jccolor.c
        jcdctmgr.c jchuff.c jcinit.c jcmainct.c jcmarker.c jcmaster.c
        jcomapi.c jcparam.c jcprepct.c jcsample.c jctrans.c jdapimin.c
        jdapistd.c jdarith.c jdatadst.c jdatasrc.c jdcoefct.c jdcolor.c
        jddctmgr.c jdhuff.c jdinput.c jdmainct.c jdmarker.c jdmaster.c
        jdmerge.c jdpostct.c jdsample.c jdtrans.c jerror.c jfdctflt.c
        jfdctfst.c jfdctint.c jidctflt.c jidctfst.c jidctint.c jquant1.c
        jquant2.c jutils.c jmemmgr.c
)

# memmgr back ends: compile only one of these into a working library
# set(SYSDEPSOURCES jmemansi.c jmemname.c jmemnobs.c jmemdos.c jmemmac.c)
set(SYSDEPSOURCES jmemansi.c)
# source files: cjpeg/djpeg/jpegtran applications, also rdjpgcom/wrjpgcom
set(APPSOURCES
        cjpeg.c djpeg.c jpegtran.c rdjpgcom.c wrjpgcom.c cdjpeg.c
        rdcolmap.c rdswitch.c transupp.c rdppm.c wrppm.c rdgif.c wrgif.c
        rdtarga.c wrtarga.c rdbmp.c wrbmp.c rdrle.c wrrle.c
)

set(SOURCES ${LIBSOURCES} ${SYSDEPSOURCES})


configure_file(${CMAKE_CURRENT_SOURCE_DIR}/jconfig.txt ${CMAKE_CURRENT_BINARY_DIR}/jconfig.h)

include_directories(
	.
	${CMAKE_CURRENT_BINARY_DIR}
)

add_library(${PROJECT} STATIC ${SOURCES})
# set_target_properties(${PROJECT} PROPERTIES OUTPUT_NAME jpeg)

# add_library(${PROJECT}.shared SHARED ${HEADERS} ${SOURCES})
# set_target_properties(${PROJECT}.shared PROPERTIES OUTPUT_NAME common)
