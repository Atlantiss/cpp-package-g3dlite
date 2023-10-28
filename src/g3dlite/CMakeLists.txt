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

add_library(g3dlite STATIC ${SOURCES_FILES})
add_library(G3D::g3dlite ALIAS g3dlite)

target_include_directories(g3dlite
    PUBLIC 
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/>
        $<INSTALL_INTERFACE:include>
)

target_compile_options(g3dlite
    INTERFACE 
        $<$<CXX_COMPILER_ID:MSVC>:/wd4996 /wd4985 /wd4244 /wd4267 /wd4619 /wd4512>)

target_link_libraries(g3dlite
  PUBLIC
    ZLIB::ZLIB
    Threads::Threads
)

# Package configuration:

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

set(INSTALL_CONFIGDIR ${CMAKE_INSTALL_LIBDIR}/cmake/${PROJECT_NAME})

configure_file(
    "${PROJECT_SOURCE_DIR}/g3dliteConfig.cmake.in"
    ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
    @ONLY
)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake
    DESTINATION
    ${INSTALL_CONFIGDIR}
)

install(
    DIRECTORY "${CMAKE_CURRENT_LIST_DIR}/include/G3D"
    DESTINATION "include"
)

install(
    TARGETS  ${PROJECT_NAME}
    EXPORT   ${PROJECT_NAME}Targets DESTINATION lib
    INCLUDES                        DESTINATION include
)

install(
    EXPORT ${PROJECT_NAME}Targets
    FILE ${PROJECT_NAME}Targets.cmake
    NAMESPACE ${PROJECT_NAME}::
    DESTINATION ${INSTALL_CONFIGDIR}
)