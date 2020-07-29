#
# Copyright (c) 2020 Nordic Semiconductor ASA
#
# SPDX-License-Identifier: LicenseRef-BSD-5-Clause-Nordic
#
cmake_minimum_required(VERSION 3.13.1)

set(NRF_SUPPORTED_BOARDS
	nrf52840dk_nrf52840
	nrf52833dk_nrf52833
)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

include(${NRFXLIB_DIR}/common.cmake)

project(openthread_cli)

target_sources(app PRIVATE src/main.c)

function(ot_libs_substitute)
      execute_process(
          COMMAND           git rev-parse HEAD
          WORKING_DIRECTORY ${openthread_SOURCE_DIR}
          RESULT_VARIABLE   git_return
          OUTPUT_VARIABLE   openthread_git_hash)
      
      list(APPEND OT_SETTINGS "OpenThread_commit=${openthread_git_hash}\n\n")
      
      # Store all OT related variables
      get_cmake_property(_variableNames VARIABLES)
      list (SORT _variableNames)
      foreach (_variableName ${_variableNames})
	  if("${_variableName}" MATCHES "^CONFIG_OPENTHREAD_.*|^OT_.*") 
		  list(APPEND OT_SETTINGS "${_variableName}=${${_variableName}}\n")
	  endif()
      endforeach()
      
      FILE(WRITE "${PROJECT_BINARY_DIR}/openthread_lib_configuration.txt" ${OT_SETTINGS})
      
      set(OPENTHREAD_LIBS
	      "${PROJECT_BINARY_DIR}/modules/openthread/build/src/core/libopenthread-ftd.a"
	      "${PROJECT_BINARY_DIR}/modules/openthread/build/src/core/libopenthread-mtd.a"
	      "${PROJECT_BINARY_DIR}/modules/openthread/build/src/core/libopenthread-radio.a"
	      "${PROJECT_BINARY_DIR}/modules/openthread/build/src/cli/libopenthread-cli-ftd.a"
	      "${PROJECT_BINARY_DIR}/modules/openthread/build/src/cli/libopenthread-cli-mtd.a"
	      "${PROJECT_BINARY_DIR}/modules/openthread/build/src/ncp/libopenthread-ncp-ftd.a"
	      "${PROJECT_BINARY_DIR}/modules/openthread/build/src/ncp/libopenthread-ncp-mtd.a"
	      "${PROJECT_BINARY_DIR}/modules/openthread/build/src/ncp/libopenthread-rcp.a"
      )

      nrfxlib_calculate_lib_path(lib_path)

      foreach(lib IN LISTS OPENTHREAD_LIBS)
	  add_custom_command(
		      TARGET app
		      COMMENT "Copying OpenThread library: ${lib}."
		      PRE_LINK
		      COMMAND ${CMAKE_COMMAND} -E copy "${lib}" "${NRFXLIB_DIR}/openthread/${lib_path}/v${OT_THREAD_VERSION}"
		      DEPENDS ${OPENTHREAD_LIBS})
      endforeach()

      add_custom_command(
	TARGET app
	COMMENT "Copying OpenThread headers."
	PRE_LINK
	COMMAND ${CMAKE_COMMAND} -E copy ${NRFXLIB_DIR}/openthread/include/openthread-config-generic.h ${PROJECT_BINARY_DIR}
	COMMAND ${CMAKE_COMMAND} -E remove ${openthread_SOURCE_DIR}/include/openthread-config-android.h
	COMMAND ${CMAKE_COMMAND} -E remove_directory -f ${NRFXLIB_DIR}/openthread/include
	COMMAND ${CMAKE_COMMAND} -E copy_directory ${openthread_SOURCE_DIR}/include ${NRFXLIB_DIR}/openthread/include
	COMMAND ${CMAKE_COMMAND} -E copy ${PROJECT_BINARY_DIR}/openthread-config-generic.h ${NRFXLIB_DIR}/openthread/include 
	COMMAND ${CMAKE_COMMAND} -E copy ${openthread_SOURCE_DIR}/examples/platforms/openthread-system.h ${NRFXLIB_DIR}/openthread/include/
	)

endfunction(ot_libs_substitute)

if(CONFIG_OPENTHREAD_LIBRARIES_SUBSTITUTE)
  ot_libs_substitute()
endif()