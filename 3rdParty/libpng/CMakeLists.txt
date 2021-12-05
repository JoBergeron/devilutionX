include(FetchContent_MakeAvailableExcludeFromAll)

if(NOT DISABLE_LTO)
  # Force CMake to raise an error if INTERPROCEDURAL_OPTIMIZATION
  # is enabled and compiler does not support IPO
  set(CMAKE_POLICY_DEFAULT_CMP0069 NEW)
endif()

if(DEVILUTIONX_STATIC_LIBPNG)
  set(PNG_LIBRARY png_static)
  set(PNG_STATIC ON)
  set(PNG_SHARED OFF)
else()
  set(PNG_LIBRARY png)
  set(PNG_STATIC OFF)
  set(PNG_SHARED ON)
endif()
set(PNG_TESTS OFF)
set(PNG_EXECUTABLES OFF)
set(SKIP_INSTALL_PROGRAMS ON)

if(IOS AND CMAKE_OSX_ARCHITECTURES STREQUAL "arm64")
  set(PNG_ARM_NEON "on")
endif()

include(FetchContent)
FetchContent_Declare(png
  URL https://github.com/diasurgical/libpng/archive/853b998ed76cbea39c2ffcd48a3fb32a396364c3.tar.gz
  URL_HASH MD5=cc78c186000fcf17ad85d67c55699fcb
)
FetchContent_MakeAvailableExcludeFromAll(png)

target_include_directories(${PNG_LIBRARY} INTERFACE
  $<BUILD_INTERFACE:${png_SOURCE_DIR}>
  $<BUILD_INTERFACE:${png_BINARY_DIR}>)

add_library(PNG::PNG ALIAS ${PNG_LIBRARY})
