
message( STATUS "Creating target colorize…" )
add_executable( colorize colorize.cpp )
target_link_libraries( colorize staticlvr )

if(PCL_FOUND)
    target_link_libraries( colorize ${PCL_LIBRARIES} )
endif(PCL_FOUND)
if( ${NABO_FOUND} )
    target_link_libraries( colorize ${NABO_LIBRARIES})
endif( ${NABO_FOUND} )
