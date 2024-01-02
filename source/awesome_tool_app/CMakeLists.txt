find_package(cmake_test_bed__state_machine)

add_executable(awesome_tool
  main.cpp
)
add_executable(my::awesome_tool ALIAS awesome_tool)
target_link_libraries(awesome_tool
  PRIVATE cmake_test_bed::state_machine
)

install(TARGETS awesome_tool
  EXPORT CMakeTestBedTargets
  RUNTIME DESTINATION "${INSTALL_BIN_DIR}" COMPONENT bin
)
