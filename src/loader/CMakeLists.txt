﻿file(GLOB loader_SRC "*.cpp")
add_executable (loader WIN32 ${loader_SRC})

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET loader PROPERTY CXX_STANDARD 20)
endif()

set(wxWidgets_ROOT_DIR "C:/wxWidgets-3.2.4")
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
  set(wxWidgets_LIB_DIR "${wxWidgets_ROOT_DIR}/lib/vc_x64_lib")  # 64-bit
else()
  set(wxWidgets_LIB_DIR "${wxWidgets_ROOT_DIR}/lib/vc_lib")      # 32-bit
endif()
set(wxWidgets_CONFIGURATION mswu)

find_package(wxWidgets REQUIRED core base OPTIONAL_COMPONENTS net)
include(${wxWidgets_USE_FILE})

target_link_libraries(loader ${wxWidgets_LIBRARIES} shared)
target_include_directories(loader PUBLIC ${wxWidgets_INCLUDE_DIRS} "src/shared")
add_definitions(-DWIN32_LEAN_AND_MEAN)
