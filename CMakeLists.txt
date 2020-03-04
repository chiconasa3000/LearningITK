cmake_minimum_required (VERSION 3.12.0)

project(DeformableRegistration)

find_package(ITK REQUIRED)
include(${ITK_USE_FILE})

if(ITKVtkGlue_LOADED)
	find_package(VTK REQUIRED)
	include(${VTK_USE_FILE})
else()
	find_package(ItkVtkGlue REQUIRED)
	include(${ItkVtkGlue_USE_FILE})
	set(Glue ItkVtkGlue)
endif()

#Librerias para CUDA
find_package(CUDA QUIET REQUIRED)

set(
	CUDA_NVCC_FLAGS
	${CUDA_NVCC_FLAGS};
	-m64 -gencode arch=compute_30,code=compute_30
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR} /usr/local/cuda-10.2/samples/common/inc)
link_directories(/usr/local/cuda-10.2/lib64)



#add_executable(DeformableRegistration DeformableRegistration15.cxx)
#target_link_libraries(DeformableRegistration ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES} -lcudart -lcublas -lcusparse)

#add_executable(DeformableRegistrationGen DeformableRegistration.cxx)
#target_link_libraries(DeformableRegistrationGen ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

#Playing with ITK BSpline

add_executable(BSplineDeformableExample CirclesBspline/exampleBSplineDeformable.cxx)
target_link_libraries(BSplineDeformableExample ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

add_executable(TransformReadWrite TransfBSplineReadWrite/transformReadWrite.cxx)
target_link_libraries(TransformReadWrite ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

add_executable(BsplineWarping1 BSplineWarping1/bsplineWarping1.cxx)
target_link_libraries(BsplineWarping1 ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

add_executable(BsplineWarping2 BSplineWarping2/bsplineWarping2.cxx)
target_link_libraries(BsplineWarping2 ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

add_executable(DefReg12_8 DefReg12_8/defReg12_8.cxx)
target_link_libraries(DefReg12_8 ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

add_executable(DefReg13 DefReg13/defReg13.cxx)
target_link_libraries(DefReg13 ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

add_executable(DefReg14 DefReg14/defReg14.cxx)
target_link_libraries(DefReg14 ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

add_executable(DefReg15 DefReg15/defReg15.cxx)
target_link_libraries(DefReg15 ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

add_executable(ChangeInfo ChangeInfo/ChangeInformationImageFilter.cxx)
target_link_libraries(ChangeInfo ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})

add_executable(DefReg4 DefReg4/defReg4.cxx)
target_link_libraries(DefReg4 ${Glue} ${VTK_LIBRARIES} ${ITK_LIBRARIES})














