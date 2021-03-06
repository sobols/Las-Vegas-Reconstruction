set(LSSR_SOURCES
    io/BaseIO.cpp
    io/ModelFactory.cpp
    io/PLYIO.cpp
    io/AsciiIO.cpp
    io/UosIO.cpp
    io/ObjIO.cpp	
    io/LasIO.cpp
    io/PCDIO.cpp
    io/PPMIO.cpp
    io/Progress.cpp
    io/Timestamp.cpp
    io/MeshBuffer.cpp
    io/PointBuffer.cpp
    io/GridIO.cpp
    io/KinectGrabber.cpp
    io/KinectIO.cpp
    io/CoordinateTransform.cpp
    io/BoctreeIO.cpp
    io/TextureIO.cpp
    display/InteractivePointCloud.cpp
    display/CoordinateAxes.cpp
    display/Renderable.cpp
    display/PointCloud.cpp
    display/MultiPointCloud.cpp
    display/StaticMesh.cpp
    display/ColorMap.cpp
    display/GroundPlane.cpp
    display/Grid.cpp
    display/Color.cpp
    display/MeshCluster.cpp
    display/GlTexture.cpp
    display/TextureFactory.cpp
    display/TexturedMesh.cpp
    reconstruction/PCLFiltering.cpp
    texture/Texture.cpp
    texture/ImageProcessor.cpp
    texture/Statistics.cpp
    texture/AutoCorr.cpp
    texture/CrossCorr.cpp
    texture/CCV.cpp
    texture/Transform.cpp
    texture/Trans.cpp
)
SET_SOURCE_FILES_PROPERTIES(io/BoctreeIO.cpp PROPERTIES COMPILE_FLAGS "-std=gnu++0x")

message(STATUS "Building static library")
add_library(staticlvr STATIC ${LSSR_SOURCES})

set_target_properties(staticlvr PROPERTIES LIBRARY_OUTPUT_DIRECTORY
    ${CMAKE_SOURCE_DIR}/lib)

target_link_libraries(staticlvr ${Boost_PROGRAM_OPTIONS_LIBRARY}
    ${Boost_SYSTEM_LIBRARY} ${Boost_THREAD_LIBRARY} ${Boost_FILESYSTEM_LIBRARY}
    ${OpenMP_CXX_FLAGS} ${OPENGL_LIBRARY} ${OpenCV_LIBS})
target_link_libraries(staticlvr laslib_static)
target_link_libraries(staticlvr obj)
target_link_libraries(staticlvr pthread)
target_link_libraries(staticlvr ${PCL_LIBRARIES})
target_link_libraries(staticlvr slam6d_static)

if ( rply_shared ) 
    target_link_libraries(staticlvr ${rply_shared})
else ( rply_shared )
    target_link_libraries(staticlvr rply_local_static)
endif ( rply_shared )

message(STATUS "Building shared library")
add_library(lvr SHARED ${LSSR_SOURCES})

set_target_properties(lvr PROPERTIES LIBRARY_OUTPUT_DIRECTORY
     ${CMAKE_SOURCE_DIR}/lib)
target_link_libraries(lvr ${Boost_PROGRAM_OPTIONS_LIBRARY}
     ${Boost_SYSTEM_LIBRARY} ${Boost_THREAD_LIBRARY} ${Boost_FILESYSTEM_LIBRARY}
     ${OpenMP_CXX_FLAGS} ${OPENGL_LIBRARY} ${OpenCV_LIBS} )
target_link_libraries(lvr laslib)
target_link_libraries(lvr obj)
target_link_libraries(lvr pthread)
target_link_libraries(lvr ${PCL_LIBRARIES})
target_link_libraries(lvr slam6d)
target_link_libraries(lvr GLU)
target_link_libraries(lvr glut)

if ( rply_shared )
     target_link_libraries(lvr ${rply_shared})
else ( rply_shared )
     target_link_libraries(lvr rply_local)
endif ( rply_shared )
