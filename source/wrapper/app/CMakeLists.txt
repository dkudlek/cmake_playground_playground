find_package(CMakeTestBed)

include_directories(${CMAKETESTBED_INCLUDE_DIRS})

get_property(dirs DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY INCLUDE_DIRECTORIES)
foreach(dir ${dirs})
  message(STATUS "CMakeTestBed dir='${dir}'")
endforeach()

add_executable(awesome_tool
  main.cpp
)
add_executable(my::awesome_tool ALIAS awesome_tool)
target_link_libraries(awesome_tool
  PRIVATE foo
)

install(TARGETS awesome_tool
  # IMPORTANT: Add the bar executable to the "export-set"
  EXPORT CMakeTestBedTargets
  RUNTIME DESTINATION "${INSTALL_BIN_DIR}" COMPONENT bin)
