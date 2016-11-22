CMAKE_MINIMUM_REQUIRED(VERSION 2.6)


#set(BUILD_TYPE Release)

# required libraries
#find_package(SuiteParse REQUIRED)
#find_package(Eigen3 REQUIRED)
#find_package(Boost COMPONENTS system thread)


# flags
add_definitions("-DENABLE_SSE") #TODO what does it do?
#set(CMAKE_CXX_FLAGS
#   "${SSE_FLAGS} -O3 -g -std=c++0x -fno-omit-frame-pointer -march=native"
#   "${SSE_FLAGS} -O3 -g -std=c++0x -fno-omit-frame-pointer"
#)

# Sources files
set(dso_SOURCE_FILES
  src/FullSystem/FullSystem.cpp
  src/FullSystem/FullSystemOptimize.cpp
  src/FullSystem/FullSystemOptPoint.cpp
  src/FullSystem/FullSystemDebugStuff.cpp
  src/FullSystem/FullSystemMarginalize.cpp
  src/FullSystem/Residuals.cpp
  src/FullSystem/CoarseTracker.cpp
  src/FullSystem/CoarseInitializer.cpp
  src/FullSystem/ImmaturePoint.cpp
  src/FullSystem/HessianBlocks.cpp
  src/FullSystem/PixelSelector2.cpp
  src/OptimizationBackend/EnergyFunctional.cpp
  src/OptimizationBackend/AccumulatedTopHessian.cpp
  src/OptimizationBackend/AccumulatedSCHessian.cpp
  src/OptimizationBackend/EnergyFunctionalStructs.cpp
  src/util/settings.cpp
  src/util/Undistort.cpp
  src/util/globalCalib.cpp

#as we won't use opencv we need the dummy object
  src/IOWrapper/ImageDisplay_dummy.cpp
  src/IOWrapper/ImageRW_dummy.cpp
)



include_directories(
  src
  thirdparty/sophus
  ${EIGEN3_INCLUDE_DIR}
) 

set(HAS_PANGOLIN 0)
set(HAS_OPENCV 0)


# compile main library.
#include_directories( ${CSPARSE_INCLUDE_DIR} ${CHOLMOD_INCLUDE_DIR}) 
add_library(dso SHARED ${dso_SOURCE_FILES})# ${dso_opencv_SOURCE_FILES} ${dso_pangolin_SOURCE_FILES})
target_link_libraries(dso PRIVATE boost_system boost_thread)
#TODO we need to link with boost
