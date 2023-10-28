set(SOURCES_FILES
    source/AABox.cpp
    source/Any.cpp
    source/AnyTableReader.cpp
    source/BinaryFormat.cpp
    source/BinaryInput.cpp
    source/BinaryOutput.cpp
    source/Box.cpp
    source/Capsule.cpp
    source/CollisionDetection.cpp
    source/CoordinateFrame.cpp
    source/Crypto.cpp
    source/Cylinder.cpp
    source/debugAssert.cpp
    source/FileSystem.cpp
    source/fileutils.cpp
    source/format.cpp
    source/g3dfnmatch.cpp
    source/g3dmath.cpp
    source/GThread.cpp
    source/Line.cpp
    source/LineSegment.cpp
    source/Log.cpp
    source/Matrix3.cpp
    source/Matrix4.cpp
    source/MemoryManager.cpp
    source/PhysicsFrame.cpp
    source/Plane.cpp
    source/prompt.cpp
    source/Quat.cpp
    source/Random.cpp
    source/Ray.cpp
    source/RegistryUtil.cpp
    source/Sphere.cpp
    source/stringutils.cpp
    source/System.cpp
    source/TextInput.cpp
    source/TextOutput.cpp
    source/Triangle.cpp
    source/uint128.cpp
    source/UprightFrame.cpp
    source/Vector2.cpp
    source/Vector3.cpp
    source/Vector4.cpp)

add_library(g3dlite ${SOURCES_FILES})
add_library(G3D::G3DLite ALIAS g3dlite)

target_include_directories(g3dlite
    PRIVATE 
        ${CMAKE_CURRENT_SOURCE_DIR}/include
    PUBLIC 
        $<INSTALL_INTERFACE:include>
)

target_link_libraries(g3dlite
  PUBLIC
    ZLIB::ZLIB
    threads
)

install(
    TARGETS g3dlite
    EXPORT g3dlite-targets
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)

file(GLOB HEADERS "${CMAKE_CURRENT_LIST_DIR}/include/*.h")
install(FILES ${HEADERS} DESTINATION "include")

include(CMakePackageConfigHelpers)

configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/g3dlite-config.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/g3dlite-config.cmake"
  INSTALL_DESTINATION "share/g3dlite"
)

install(
  FILES "${CMAKE_CURRENT_BINARY_DIR}/g3dlite-config.cmake"
  DESTINATION "share/g3dlite"
)

install(
    EXPORT g3dlite-targets
    DESTINATION share/g3dlite
    NAMESPACE G3D::
)
