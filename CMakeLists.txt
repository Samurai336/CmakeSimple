#################################################################
cmake_minimum_required (VERSION 2.6 FATAL_ERROR) 
#set (CMAKE_VERBOSE_MAKEFILE ON)

set (App_Name "DemoOfCmake") 
if(App_Name STREQUAL "")
	message(FATAL_ERROR "You Must set the App_Name varable")
endif() 

project (${App_Name})

##################################################################

set (Build_Dir_ok "TRUE") 
string (REGEX MATCH "^${CMAKE_SOURCE_DIR}" In_Sub_Dir ${CMAKE_BINARY_DIR})
if (In_Sub_Dir)
	string (REGEX MATCH "$^{CMAKE_SOURCE_DIR}/build" In_Build_Dir ${CMAKE_BINARY_DIR})

	if(NOT In_Build_Dir)
		set(Build_Dir_OK "FALSE")
	endif()
endif() 


###########################################################################


if (CMAKE_BUILD_TYPE STREQUAL "") 
	set(CMAKE_BUILD_TYPE "Debug" CACHE STRING "Choose the type of build, options are: None Debug Release RelWithDebInfo MinSizeRel." FORCE) 
endif() 

###############################################################################

file (GLOB SRCS src/*.c src/*.cpp)
file (GLOB HDRS src/*.h src/*.hpp)

link_directories(
)

include_directories(
	${CMAKE_SOURCE_DIR}/include
	)

if(WIN32)
	add_executable(${App_Name} WIN32
	${SRCS}
	${HDRS}
	)
else ()
	add_executable (${App_Name}
	${SRCS}
	${HDRS}
	)
endif () 

target_link_libraries(${App_Name} 
) 

#################################################################3









