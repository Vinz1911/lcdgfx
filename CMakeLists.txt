cmake_minimum_required(VERSION 3.5)

file(GLOB_RECURSE SOURCE_FILES src/*.cpp src/*.c)
file(GLOB_RECURSE HEADER_FILES src/*.h)
file(GLOB_RECURSE INL_FILES src/*.inl)

if (NOT DEFINED COMPONENT_DIR)
    project(lcdgfx)
    include_directories(src)

    add_library(lcdgfx SHARED ${HEADER_FILES} ${SOURCE_FILES} ${INL_FILES})
    install(TARGETS lcdgfx LIBRARY DESTINATION /usr/local/lib ARCHIVE DESTINATION /usr/local/lib RUNTIME DESTINATION /usr/local/bin)
    install(DIRECTORY src/ DESTINATION /usr/local/include/lcdgfx FILES_MATCHING PATTERN "*.h" PATTERN "*.inl")
else()
    idf_component_register(SRCS ${SOURCE_FILES} INCLUDE_DIRS "src" REQUIRES driver)
endif()