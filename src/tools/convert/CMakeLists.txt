add_executable( convertmodel Convert.cpp Options.cpp )
target_link_libraries( convertmodel staticlvr )

if(PCL_FOUND)
    target_link_libraries( convertmodel ${PCL_LIBRARIES} )
endif(PCL_FOUND)
