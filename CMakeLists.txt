cmake_minimum_required (VERSION 3.0.0)
project (EditLine)
set (EditLine_VERSION_MAJOR 2)
set (EditLine_VERSION_MINOR 2)
if(NOT DEFINED LIB_SUFFIX)
  if(CMAKE_SIZEOF_VOID_P MATCHES 4)
    set(LIB_SUFFIX "32")
  else()
    set(LIB_SUFFIX "64")
  endif()
endif()
configure_file (
  "${PROJECT_SOURCE_DIR}/config.h.in"
  "${PROJECT_BINARY_DIR}/config.h"
)
add_subdirectory (src)
