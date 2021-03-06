cmake_minimum_required(VERSION 3.3 FATAL_ERROR)

project(vtkThreeViewDrawing)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")

find_package(VTK)
if (NOT VTK_FOUND)
  message("Skipping vtkThreeViewDrawing: ${VTK_NOT_FOUND_MESSAGE}")
  return ()
endif()
message (STATUS "VTK_VERSION: ${VTK_VERSION}")
if (VTK_VERSION VERSION_LESS "8.90.0")
  # old system
  include(${VTK_USE_FILE})
  add_executable(vtkThreeViewDrawing MACOSX_BUNDLE vtkThreeViewDrawing.cxx )
  target_link_libraries(vtkThreeViewDrawing PRIVATE ${VTK_LIBRARIES})
else ()
  # include all components
  add_executable(vtkThreeViewDrawing MACOSX_BUNDLE vtkThreeViewDrawing.cxx )
  target_link_libraries(vtkThreeViewDrawing PRIVATE ${VTK_LIBRARIES})
  # vtk_module_autoinit is needed
  vtk_module_autoinit(
    TARGETS vtkThreeViewDrawing
    MODULES ${VTK_LIBRARIES}
    )
endif () 