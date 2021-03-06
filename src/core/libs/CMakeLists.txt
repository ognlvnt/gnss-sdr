# Copyright (C) 2012-2015  (see AUTHORS file for a list of contributors)
#
# This file is part of GNSS-SDR.
#
# GNSS-SDR is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# GNSS-SDR is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with GNSS-SDR. If not, see <http://www.gnu.org/licenses/>.
#

add_subdirectory(supl)

if(OPENSSL_FOUND)
    add_definitions( -DUSE_OPENSSL_FALLBACK=1 )
endif(OPENSSL_FOUND)

set(CORE_LIBS_SOURCES 
    ini.cc 
    INIReader.cc 
    string_converter.cc
    gnss_sdr_supl_client.cc
)
	
include_directories(
    $(CMAKE_CURRENT_SOURCE_DIR)
    ${CMAKE_SOURCE_DIR}/src/core/system_parameters
    ${CMAKE_SOURCE_DIR}/src/core/libs/supl
    ${CMAKE_SOURCE_DIR}/src/core/libs/supl/asn-rrlp
    ${CMAKE_SOURCE_DIR}/src/core/libs/supl/asn-supl
    ${GLOG_INCLUDE_DIRS}
    ${GFlags_INCLUDE_DIRS}
    ${Boost_INCLUDE_DIRS}
)

file(GLOB CORE_LIBS_HEADERS "*.h")
list(SORT CORE_LIBS_HEADERS)
add_library(rx_core_lib ${CORE_LIBS_SOURCES} ${CORE_LIBS_HEADERS})
source_group(Headers FILES ${CORE_LIBS_HEADERS})
target_link_libraries(rx_core_lib supl_library) 
