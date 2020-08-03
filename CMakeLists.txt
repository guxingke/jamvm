cmake_minimum_required(VERSION 3.5)
project(jamvm C)

enable_language(C ASM)

set(CMAKE_C_STANDARD 99)

if (CMAKE_BUILD_TYPE MATCHES "Debug")
    ADD_DEFINITIONS(-D_DEBUG -D__JVM_DEBUG__)
    message("this is a debug compile")
endif ()

include_directories(
        src/
        src/os
        src/os/linux
        src/os/linux/x86_64
        src/interp/
        src/interp/engine
        src/classlib
        src/classlib/gnuclasspath
)

set(SOURCE_FILES
        src/access.c
        src/alloc.c
        src/alloc.h
        src/annotations.h
        src/arch.h
        src/cast.c
        src/class.c
        src/class.h
        src/classlib-defs.h
        src/classlib-excep.h
        src/classlib-symbol.h
        src/classlib.h
        src/config.h
        src/dll.c
        src/dll_ffi.c
        src/excep.c
        src/excep.h
        src/execute.c
        src/frame.c
        src/frame.h
        src/hash.c
        src/hash.h
        src/hooks.c
        src/init.c
        src/jam.c
        src/jam.h
        src/jni-internal.h
        src/jni-stubs.c
        src/jni.c
        src/jni.h
        src/lock.c
        src/lock.h
        src/natives.c
        src/natives.h
        src/properties.c
        src/properties.h
        src/reflect.c
        src/reflect.h
        src/resolve.c
        src/shutdown.c
        src/sig.c
        src/sig.h
        src/string.c
        src/stubs.c
        src/stubs.h
        src/symbol.c
        src/symbol.h
        src/thread.c
        src/thread.h
        src/time.c
        src/utf8.c
        src/zip.c
        src/zip.h

        # os
        src/os/linux/os.c
        src/os/linux/x86_64/callNative.S
        src/os/linux/x86_64/init.c
        src/os/linux/x86_64/dll_md.c

        # interpreter
        src/interp/engine/interp.h
        src/interp/engine/interp-indirect.h
        src/interp/engine/interp.c

        # classpath
        src/classlib/gnuclasspath/alloc.c
        src/classlib/gnuclasspath/annotations.c
        src/classlib/gnuclasspath/class.c
        src/classlib/gnuclasspath/dll.c
        src/classlib/gnuclasspath/excep.c
        src/classlib/gnuclasspath/frame.c
        src/classlib/gnuclasspath/gnuclasspath.h
        src/classlib/gnuclasspath/jni.c
        src/classlib/gnuclasspath/natives.c
        src/classlib/gnuclasspath/properties.c
        src/classlib/gnuclasspath/reflect.c
        src/classlib/gnuclasspath/thread.c
        )

MESSAGE(STATUS "platform: ${CMAKE_SYSTEM_NAME}")

add_executable(jamvm ${SOURCE_FILES})
TARGET_LINK_LIBRARIES(jamvm pthread z dl m)