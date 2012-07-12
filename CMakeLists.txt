cmake_minimum_required(VERSION 2.6)

PROJECT(InteractivePatchMatch)
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=gnu++0x")

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})

FIND_PACKAGE(Qt4 REQUIRED)
INCLUDE(${QT_USE_FILE})

FIND_PACKAGE(ITK REQUIRED)
INCLUDE(${USE_ITK_FILE})

FIND_PACKAGE(VTK REQUIRED)
INCLUDE(${USE_VTK_FILE})

QT4_WRAP_UI(UISrcs NNFieldInspector.ui)
QT4_WRAP_CPP(MOCSrcs NNFieldInspector.h)

add_subdirectory(PatchMatch)
add_subdirectory(ITKVTKHelpers)
add_subdirectory(ITKVTKCamera)
add_subdirectory(Layer)
add_subdirectory(VTKHelpers)

add_executable(NNFieldInspector NNFieldInspectorDriver.cpp
NNFieldInspector.cpp
PointSelectionStyle2D.cpp
${UISrcs} ${MOCSrcs})

TARGET_LINK_LIBRARIES(NNFieldInspector ${VTK_LIBRARIES} ${ITK_LIBRARIES}
VTKHelpers ITKVTKCamera ITKVTKHelpers ITKHelpers Layer)