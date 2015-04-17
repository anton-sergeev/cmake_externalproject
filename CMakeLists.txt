cmake_minimum_required(VERSION 2.8)
include(ExternalProject)

set(EXTERNALS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/externals)

set(JPEG_VERSION "9a")
set(JPEG_TARBALL_URL http://ijg.org/files/jpegsrc.v${JPEG_VERSION}.tar.gz)
set(JPEG_TARBALL ${CMAKE_CURRENT_SOURCE_DIR}/tarballs/jpegsrc.v${JPEG_VERSION}.tar.gz)
set(JPEG_DIR ${EXTERNALS_DIR}/jpeg-${JPEG_VERSION})


if(NOT EXISTS "${JPEG_TARBALL}")
    file(DOWNLOAD ${JPEG_TARBALL_URL} ${JPEG_TARBALL})
endif()
add_custom_target(jpeg-download DEPENDS ${JPEG_TARBALL})

ExternalProject_Add(
    jpeg-build
    DEPENDS jpeg-download
    BINARY_DIR ${CMAKE_BINARY_DIR}/externals/jpeg-${JPEG_VERSION}
    URL ${JPEG_TARBALL}
    SOURCE_DIR ${JPEG_DIR}
    CMAKE_ARGS ""
    UPDATE_COMMAND cmake -E copy_directory ${EXTERNALS_DIR}/jpeg-${JPEG_VERSION}-overlay/. ${JPEG_DIR}
    INSTALL_COMMAND ""
    TEST_COMMAND ""
)
