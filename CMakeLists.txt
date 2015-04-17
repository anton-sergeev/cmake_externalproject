cmake_minimum_required(VERSION 2.8)
include(ExternalProject)

set(EXTERNALS_DIR ${CMAKE_CURRENT_SOURCE_DIR}/externals)

set(JPEG_VERSION "9a")
set(JPEG_URI http://ijg.org/files/jpegsrc.v${JPEG_VERSION}.tar.gz)
set(JPEG_DIR ${EXTERNALS_DIR}/jpeg-${JPEG_VERSION})

ExternalProject_Add(
    jpeg
    STAMP_DIR ${CMAKE_BINARY_DIR}/externals/jpeg-pre
    BINARY_DIR ${CMAKE_BINARY_DIR}/externals/jpeg-${JPEG_VERSION}
    URL ${JPEG_URI}
    SOURCE_DIR ${JPEG_DIR}
    DOWNLOAD_DIR ${CMAKE_CURRENT_SOURCE_DIR}/tarballs
    CMAKE_ARGS ""
    UPDATE_COMMAND cmake -E copy_directory ${EXTERNALS_DIR}/jpeg-${JPEG_VERSION}-overlay/. ${JPEG_DIR}
    INSTALL_COMMAND ""
    TEST_COMMAND ""
)
