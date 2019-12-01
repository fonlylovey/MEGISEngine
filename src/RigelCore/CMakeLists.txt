# Set porject name
set(TargetName RigelCore)
string(TOUPPER ${TargetName} TargetNameUP)

# Find includes in corresponding build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(Qt5Core)

# Find all Files
set(headers
			Export.h
			OECore.h
			FileUtils.h
			MEMath.h
			)

set(sources InputLib.cpp
			OECore.cpp
			FileUtils.cpp
			MEMath.cpp
			)

# add definitions,unicode and export
add_definitions(-DUNICODE -D_UNICODE -D${TargetNameUP}_EXPORTS)

# Set porject filiter
source_group("Header Files" FILES ${headers})

#
add_library(${TargetName} SHARED ${sources} ${headers})

# .
target_link_libraries(${TargetName} OpenThreads.lib)

INSTALL(
    FILES       ${headers}
    DESTINATION include/${TargetName}
)
INSTALL(
		TARGETS ${TargetName}
		RUNTIME DESTINATION bin
		LIBRARY DESTINATION bin
		ARCHIVE DESTINATION lib
	)