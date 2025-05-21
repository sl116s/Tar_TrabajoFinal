cmake_minimum_required(VERSION 3.0.2)
project(examples)

# pull in catkin and your quadruped lib
find_package(catkin REQUIRED COMPONENTS
  roscpp
  quadruped
)

# find the system BLAS/LAPACK backends (MKL, OpenBLAS, etc)
find_package(BLAS   REQUIRED)
find_package(LAPACK REQUIRED)

catkin_package(
  CATKIN_DEPENDS roscpp quadruped
  DEPENDS        BLAS LAPACK
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

# list of examples
add_executable(example_a1_real  example_a1_real/example_a1_real.cpp)
add_executable(example_a1_sim   example_a1_sim/example_a1_sim.cpp)
add_executable(example_lite3_real example_lite3_real/example_lite3_real.cpp)
add_executable(example_lite3_sim  example_lite3_sim/example_lite3_sim.cpp)
add_executable(example_keyboard example_keyboard/example_keyboard.cpp)

# helper macro to avoid repetition
macro(link_example tgt)
  target_link_libraries(${tgt}
    ${catkin_LIBRARIES}
    ${BLAS_LIBRARIES}
    ${LAPACK_LIBRARIES}
  )
endmacro()

link_example(example_a1_real)
link_example(example_a1_sim)
link_example(example_lite3_real)
link_example(example_lite3_sim)
link_example(example_keyboard)
