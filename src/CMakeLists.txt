cmake_minimum_required(VERSION 2.6 FATAL_ERROR)
project(cs344)

find_package(OpenCV REQUIRED)
find_package(CUDA REQUIRED)

link_libraries(${OpenCV_LIBS} )

set (EXECUTABLE_OUTPUT_PATH "${CMAKE_BINARY_DIR}/bin/")

if(CUDA_FOUND)
  set(CUDA_NVCC_FLAGS "
    -gencode;arch=compute_37,code=compute_37;
    -gencode;arch=compute_50,code=compute_50;
    -gencode;arch=compute_61,code=compute_61;
    -gencode;arch=compute_75,code=compute_75;
  ")

  # add -Wextra compiler flag for gcc compilations
  if (UNIX)
    set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS} "-Xcompiler -Wextra")
  endif (UNIX)

  # add debugging to CUDA NVCC flags.  For NVidia's NSight tools.
  set(CUDA_NVCC_FLAGS_DEBUG ${CUDA_NVCC_FLAGS_DEBUG} "-G")

  add_subdirectory (HW1)
  add_subdirectory (HW2)
  add_subdirectory (HW3)
  add_subdirectory (HW4)
  add_subdirectory (HW5)
  add_subdirectory (HW6)
else(CUDA_FOUND)
  message("CUDA is not installed on this system.")
endif()
