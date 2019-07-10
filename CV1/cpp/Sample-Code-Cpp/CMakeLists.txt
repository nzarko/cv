cmake_minimum_required(VERSION 2.8.12)

PROJECT(sampleCode)

######################## EDIT IF REQUIRED ####################
###Uncomment the line below and specify the path to OpenCV directory i.e. the path to the OpenCVConfig.cmake file. Check the examples given below.

#SET(OpenCV_DIR Enter-the-path-of-OpenCV-installation-on-your-system)

if(UNIX)
    SET(OpenCV_DIR /home/nick/OpenCV/installation/OpenCV-4.1.0/lib/cmake/opencv4)
ENDIF(UNIX)

################### OpenCV_DIR Examples  #####################

### MACOS : /usr/local/Cellar/opencv/4.1.0/share/OpenCV/

### UBUNTU : /usr/local/share/OpenCV/

### WINDOWS : C:\Users\yourname\Documents\opencv-4.1.0\build\install

##############################################################

###################   ***DO NOT EDIT***  #####################

#############  Common Instructions for all Users  ############
find_package( OpenCV REQUIRED )

include_directories( ${OpenCV_INCLUDE_DIRS})

if(MSVC)
 set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /EHsc /W3")
# SET(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MT")
 set(CompilerFlags
        CMAKE_CXX_FLAGS
        CMAKE_CXX_FLAGS_DEBUG
        CMAKE_CXX_FLAGS_RELEASE
        CMAKE_CXX_FLAGS_MINSIZEREL
        CMAKE_CXX_FLAGS_RELWITHDEBINFO
        CMAKE_C_FLAGS
        CMAKE_C_FLAGS_DEBUG
        CMAKE_C_FLAGS_RELEASE
        CMAKE_C_FLAGS_MINSIZEREL
        CMAKE_C_FLAGS_RELWITHDEBINFO
        )
foreach(CompilerFlag ${CompilerFlags})
  string(REPLACE "/MD" "/MT" ${CompilerFlag} "${${CompilerFlag}}")
  set(${CompilerFlag} "${${CompilerFlag}}" CACHE STRING "msvc compiler flags" FORCE)
  message("MSVC flags: ${CompilerFlag}:${${CompilerFlag}}")
endforeach()
endif(MSVC)

MACRO(add_example name)
  ADD_EXECUTABLE(${name} ${name}.cpp)
  TARGET_LINK_LIBRARIES(${name} ${OpenCV_LIBS} )
ENDMACRO()

add_example(sampleCode)
