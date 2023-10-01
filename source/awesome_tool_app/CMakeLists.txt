find_package(cmake_test_bed__state_machine)

get_target_property(va cmake_test_bed::state_machine INTERFACE_INCLUDE_DIRECTORIES)
message("va: ${va}")

message("blah ||| ${cmake_test_bed__state_machine_FOUND}")
message(STATUS "YourLibrary_INCLUDE_DIRS: ${IMPORTED_LOCATION_RELEASE}")
foreach(dir ${IMPORTED_LOCATION_RELEASE})
    message(STATUS "Include directory: ${dir}")
endforeach()
add_executable(awesome_tool
  main.cpp
)
add_executable(my::awesome_tool ALIAS awesome_tool)
target_link_libraries(awesome_tool
  PRIVATE cmake_test_bed::state_machine
)

install(TARGETS awesome_tool
  # IMPORTANT: Add the bar executable to the "export-set"
  EXPORT CMakeTestBedTargets
  RUNTIME DESTINATION "${INSTALL_BIN_DIR}" COMPONENT bin)
