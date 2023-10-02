This used to test that cmake_playground actually worked and we can include it from a different repository if we set the path correctly. 


[TOC]

# How-To use ``foo`` from ``CMakeTestBed``
- First, we need to close and build cmake_playground
- Build the target install via the instructaion 
- Add the path to installed cmake folder to your PATH variable
- Now we build this repository and this is the most important line: 
  ```cmake
  find_package(cmake_test_bed__state_machine)
  ```
- If we can find the package, we just need to do this step:
  ```cmake
  target_link_libraries(awesome_tool
    PRIVATE cmake_test_bed::state_machine
  )
  ```
- and then we can build:
  ```bash
  mkdir build          # Create a directory to hold the build output.
  cd build
  cmake .. -DCMAKE_INSTALL_PREFIX=../install # Set install folder to PROJECT_ROOT/install
  cmake --build . --config Release --target install  # Build release and trigger install procedure
  ```

# CI with Gitlab Runner
- We need to cloe cmake_playground with the CI token like this: 
  ```sh
  git clone http://gitlab-ci-token:${CI_JOB_TOKEN}@<gitlab-host>/dkudlek/cmake_playground.git
  ```
