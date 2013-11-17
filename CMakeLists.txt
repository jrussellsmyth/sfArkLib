cmake_minimum_required (VERSION 2.8)
project (sfArkLib)

#project source files
set(SFARK_SOURCES
	sfklCoding.cpp 
	sfklCrunch.cpp 
	sfklDiff.cpp 
	sfklFile.cpp 
	sfklLPC.cpp 
	sfklString.cpp 
	sfklZip.cpp
)

#include/link to ZLIB
find_package( ZLIB REQUIRED )
include_directories( ${ZLIB_INCLUDE_DIRS} )

add_library(stark SHARED ${SFARK_SOURCES})
target_link_libraries(sfark ${ZLIB_LIBRARIES} )

if(APPLE)
#linker command for OSX must be specified
set_target_properties(sfark PROPERTIES LINK_FLAGS "-flat_namespace -undefined suppress")
endif(APPLE)

install(TARGETS sfark LIBRARY DESTINATION lib)	