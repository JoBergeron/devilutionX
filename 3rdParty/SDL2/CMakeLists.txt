if(DEVILUTIONX_STATIC_SDL2)
  set(BUILD_SHARED_LIBS OFF)
  set(SDL_SHARED OFF)
  set(SDL_STATIC ON)
  if(PIE)
    set(SDL_STATIC_PIC ON)
  endif()
else()
  set(BUILD_SHARED_LIBS ON)
  set(SDL_SHARED ON)
  set(SDL_STATIC OFF)
endif()

include(FetchContent_MakeAvailableExcludeFromAll)
include(FetchContent)
FetchContent_Declare(SDL2
    URL https://github.com/libsdl-org/SDL/archive/563ef2aeb23ea722b773be8f5d216c53ad3eec18.tar.gz
    URL_HASH MD5=d3bab22e1c7d8b7e897bf00310fefd82
)
FetchContent_MakeAvailableExcludeFromAll(SDL2)

if(TARGET SDL2::SDL2-static)
  add_library(SDL2::SDL2 ALIAS SDL2-static)
endif()
