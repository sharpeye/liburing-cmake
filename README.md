# liburing-cmake
usage:
```cmake
...

include(FetchContent)

FetchContent_Declare(
    liburing_cmake
    GIT_REPOSITORY https://github.com/sharpeye/liburing-cmake.git
    GIT_TAG main
)

FetchContent_MakeAvailable(liburing_cmake)

...

target_link_libraries(foo PRIVATE liburing)

...

```
