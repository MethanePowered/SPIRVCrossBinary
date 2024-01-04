if (POLICY CMP0114)
    # 'ExternalProject' step targets fully adopt their steps, support new CMake build system
    cmake_policy(SET CMP0114 NEW)
endif()

set(TARGET SPIRV)

include(ExternalProject)

if (WIN32)

    set(BINARIES_MD5 6b97e67c77be412b0604cc7d2f12c677)
    set(BINARIES_DIR ${CMAKE_CURRENT_SOURCE_DIR}/binaries/Windows)

elseif(APPLE)

    set(BINARIES_MD5 2a7c758626b26b9540c290c0643c136d)
    set(BINARIES_DIR ${CMAKE_CURRENT_SOURCE_DIR}/binaries/MacOS)

else()
    
    message(FATAL_ERROR "SPIRV Cross is not available for Linux")

endif()

ExternalProject_Add(${TARGET}
    URL ${BINARIES_DIR}.zip
    URL_MD5 ${BINARIES_MD5}
    SOURCE_DIR ${BINARIES_DIR}
    BUILD_IN_SOURCE TRUE
    EXCLUDE_FROM_ALL TRUE
    DOWNLOAD_EXTRACT_TIMESTAMP TRUE
    CONFIGURE_COMMAND ""
    BUILD_COMMAND ""
    STEP_TARGETS build
)