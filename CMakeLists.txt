cmake_minimum_required(VERSION 2.8.10)

project(NemaTode)

set(TARGET_NAME NemaTode)
add_library(${TARGET_NAME} STATIC
    include/nmeaparse/Event.h
    include/nmeaparse/GPSFix.h
    include/nmeaparse/GPSService.h
    include/nmeaparse/nmea.h
    include/nmeaparse/NMEACommand.h
    include/nmeaparse/NMEAParser.h
    include/nmeaparse/NumberConversion.h
    src/GPSFix.cpp
    src/GPSService.cpp
    src/NMEACommand.cpp
    src/NMEAParser.cpp
    src/NumberConversion.cpp
)

target_include_directories(${TARGET_NAME}
    PUBLIC
        $<INSTALL_INTERFACE:include>
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
)

target_compile_features(${TARGET_NAME} PUBLIC cxx_std_11)

install(TARGETS ${TARGET_NAME}
    EXPORT ${TARGET_NAME}-export
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
)

install(DIRECTORY include/ DESTINATION include)

install(EXPORT ${TARGET_NAME}-export
  FILE
    ${TARGET_NAME}-targets.cmake
  NAMESPACE
    NemaTode::
  DESTINATION
    cmake/${TARGET_NAME}
)
