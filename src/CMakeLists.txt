include_directories("${PROJECT_SOURCE_DIR}/src")
include_directories("${PROJECT_BINARY_DIR}")
include(GenerateExportHeader)

macro(generate TYPE DEST)
	add_custom_command(OUTPUT ${DEST} 
		COMMAND AWK=${AWK} sh makelist ${TYPE} ${ARGN} > ${DEST} 
    	WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}		
		DEPENDS ${ARGN}
		VERBATIM)
endmacro()

set(HDRS vi.h emacs.h common.h)
set(SRCS vi.c emacs.c common.c)

generate( -h  vi.h     vi.c    )
generate( -h  emacs.h  emacs.c )
generate( -h  common.h common.c)
generate( -fh fcns.h   ${HDRS} )
generate( -fc func.h   ${HDRS} )
generate( -bh help.h   ${SRCS} )
	
add_library(edit STATIC 
	chared.c 
	common.c 
	el.c 
	eln.c 
	emacs.c 
	hist.c 
	keymacro.c 
	map.c 
	chartype.c 
	parse.c 
	prompt.c 
	read.c 
	refresh.c 
	search.c 
	sig.c 
	terminal.c 
	tty.c 
	vi.c 
	wcsdup.c
	tokenizer.c 
	tokenizern.c 
	history.c 
	historyn.c 
	filecomplete.c 
	readline.c
	literal.c

	chared.h  
	el.h 
	hist.h 
	histedit.h 
	keymacro.h 
	map.h 
	chartype.h 
	parse.h
	prompt.h 
	read.h 
	refresh.h
	search.h 
	sig.h 
	sys.h 
	terminal.h 
	tty.h 
	vis.h 
	filecomplete.h 
	editline/readline.h
	literal.h

	fcns.h
	help.h
	func.h
)

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
target_sources(edit PRIVATE strlcpy.c)
endif()


if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
target_sources(edit PRIVATE strlcat.c)
endif()


if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
target_sources(edit PRIVATE getline.c)
endif()

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
target_sources(edit PRIVATE vis.c vis.h)
endif()

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
target_sources(edit PRIVATE unvis.c)
endif()


set_target_properties(edit PROPERTIES PREFIX "")
GENERATE_EXPORT_HEADER(edit
  BASE_NAME edit
  EXPORT_MACRO_NAME edit_EXPORT
  EXPORT_FILE_NAME edit_Export.h
  STATIC_DEFINE edit_BUILT_AS_STATIC
)

#install (TARGETS edit edit_test edit_test_dll
#  DESTINATION "${CMAKE_SOURCE_DIR}/bin${LIB_SUFFIX}")
#install (TARGETS edit_static
#  DESTINATION "${CMAKE_SOURCE_DIR}/lib${LIB_SUFFIX}")
#install (FILES editline/readline.h
#  DESTINATION "${CMAKE_SOURCE_DIR}/include/editline")
#string(TOUPPER "${CMAKE_BUILD_TYPE}" uppercase_CMAKE_BUILD_TYPE)
#if (MSVC AND uppercase_CMAKE_BUILD_TYPE MATCHES "DEBUG")
#  install (FILES ${CMAKE_CURRENT_BINARY_DIR}/Debug/edit_static.pdb
#    DESTINATION "${CMAKE_SOURCE_DIR}/lib${LIB_SUFFIX}")
#  install (FILES ${CMAKE_CURRENT_BINARY_DIR}/Debug/edit.pdb
#    DESTINATION "${CMAKE_SOURCE_DIR}/bin${LIB_SUFFIX}")
#endif()
