#==============================================================================================================
# options
#==============================================================================================================
option(METAKIT_BUILD_STATIC_LIBRARY "Build metakit statically" OFF)
option(METAKIT_USE_SYSTEM_STL "Enable to build with system STL" OFF)

#==============================================================================================================
# retrieve sources
#==============================================================================================================
set(metakit_SOURCES
    column.cpp
    custom.cpp
    derived.cpp
    fileio.cpp
    field.cpp
    format.cpp
    handler.cpp
    persist.cpp
    remap.cpp
    store.cpp
    string.cpp
    table.cpp
    univ.cpp
    view.cpp
    viewx.cpp)

#==============================================================================================================
# Enable to build with system STL
#==============================================================================================================
if (METAKIT_USE_SYSTEM_STL)
	add_definitions(-Dq4_STD)
	list(APPEND metakit_SOURCES std.cpp)
endif()

#==============================================================================================================
# prepare to library bundle
#==============================================================================================================
if(METAKIT_BUILD_STATIC_LIBRARY)
    add_library(metakit STATIC ${metakit_SOURCES})
else()
    add_library(metakit SHARED ${metakit_SOURCES})
endif()

add_library(metakit::metakit ALIAS metakit)

target_include_directories(metakit PUBLIC "../include/" "../configs/common/")

#==============================================================================================================
# setup installation rules
#==============================================================================================================
include(GNUInstallDirs)
install(TARGETS metakit
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR})
