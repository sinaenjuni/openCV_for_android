
cmake_minimum_required(VERSION 3.4.1)

set(pathPROJECT C:/github/Hackathon/20190701/Test1) # 수정필요
set(pathOPENCV ${pathPROJECT}/opencv)
set(pathLIBOPENCV_JAVA ${pathOPENCV}/native/libs/${ANDROID_ABI}/libopencv_java4.so)

set(CMAKE_VERBOSE_MAKEFILE on)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++11")

include_directories(${pathOPENCV}/native/jni/include)


add_library( # Sets the name of the library.
        native-lib

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        ${pathPROJECT}/app/src/main/cpp/native-lib.cpp )



add_library( lib_opencv SHARED IMPORTED )

set_target_properties(lib_opencv PROPERTIES IMPORTED_LOCATION ${pathLIBOPENCV_JAVA})


find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log )


target_link_libraries( # Specifies the target library.
        native-lib

        lib_opencv

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib} )
