cmake_minimum_required (VERSION 3.8)

if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

set(CMAKE_CXX_STANDARD 17)

if(CMAKE_C_BYTE_ORDER STREQUAL "LITTLE_ENDIAN")
  set (MD5_BIG_ENDIAN 0)
elseif(CMAKE_C_BYTE_ORDER STREQUAL "BIG_ENDIAN")
  set (MD5_BIG_ENDIAN 1)
else()
  set (MD5_BIG_ENDIAN 0)
endif()
set (MD5_DEBUG 0)
configure_file(src/conf.h.in src/conf.h @ONLY)
project(MD5)

add_library(MD5
    src/md5.cpp
)
include_directories(${CMAKE_CURRENT_BINARY_DIR}/src)
