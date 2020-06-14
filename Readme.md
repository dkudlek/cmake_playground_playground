CMake Playground Playground
====
[TOC]

# How-To use ``foo`` from ``CMakeTestBed``
- Clone [cmake_playground](http://gitlab.vnet.kudlek.online/dkudlek/cmake_playground)
- build it with ``mkdir build && cmake .. && cmake . && make``
- create the standard CMake project setup
- For the excutable which ueses ``foo`` add at the top:

    ```cmake
    find_package(CMakeTestBed)

    include_directories(${CMAKETESTBED_INCLUDE_DIRS})
    ```

- And linke the library ``foo`` from ``CMakeTestBed``:
    ```cmake
    target_link_libraries(awesome_tool
      PRIVATE foo
    )
    ```


# CI multi repo build
https://stackoverflow.com/questions/32995578/how-to-access-multiple-repositories-in-ci-build
- use ssh keys --> needs to be passed from runner to actual image


- put the whole ssh key into the variable at ``prject > settings > CI > variables``
- public deploy key has to be ``enabled`` for each project
