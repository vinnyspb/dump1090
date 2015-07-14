cmake_minimum_required (VERSION 2.8)

project (dump1090)

find_library(PTHREAD_LIBRARY pthread)
find_library(RTLSDR_LIBRARY rtlsdr PATHS /usr/lib/fr24 NO_DEFAULT_PATH)
find_library(M_LIBRARY m)

set(common_HDR
    anet.h
    coaa.h
    winstubs.h
)

set(common_SRC
    anet.c
    interactive.c
    mode_ac.c
    mode_s.c
    net_io.c
)

set(dump1090_SRC
    ${common_SRC}
    dump1090.c
)

set(view1090_SRC
    ${common_SRC}
    view1090.c
)

set(dump1090_HDR
    ${common_HDR}
    dump1090.h
)

set(view1090_HDR
    ${common_HDR}
    view1090.h
)

set(common_dependencies
    ${RTLSDR_LIBRARY}
    ${PTHREAD_LIBRARY}
    ${M_LIBRARY}
)

add_executable(dump1090 ${dump1090_HDR} ${dump1090_SRC})
add_executable(view1090 ${view1090_HDR} ${view1090_SRC})

include_directories(dump1090 rtlsdr)
include_directories(view1090 rtlsdr)

target_link_libraries(dump1090 ${common_dependencies})
target_link_libraries(view1090 ${common_dependencies})
