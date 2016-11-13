include_directories(
  include/
)

# PvcChair Hardware Interface
add_library(pvcchair_hw_interface
  src/pvcchair_hw_interface.cpp
)
target_link_libraries(pvcchair_hw_interface
  generic_hw_interface
  ${catkin_LIBRARIES}
)

# Main control executable
add_executable(pvcchair_hw_main src/pvcchair_hw_main.cpp)
target_link_libraries(pvcchair_hw_main
  pvcchair_hw_interface
  generic_hw_control_loop
  ${catkin_LIBRARIES}
)

## Install ------------------------------------------------------------

# Install libraries
install(TARGETS
    pvcchair_hw_interface
  LIBRARY DESTINATION
    ${CATKIN_PACKAGE_LIB_DESTINATION}
)

# Install executables
install(TARGETS
    pvcchair_hw_main
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

# Install header files
install(DIRECTORY include/pvcchair_control/   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})
