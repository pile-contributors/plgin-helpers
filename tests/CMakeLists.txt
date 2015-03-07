# ============================================================================
#
# This file hosts all tests.
#
# If INCLUDE_PILE_SOURCES_DIRECTLY is ON then PLGIN_SOURCES and
# PLGIN_HEADERS are defined we add them to the executable. PLGIN_LIBRARY
# is empty.
#
# On the other hand if INCLUDE_PILE_SOURCES_DIRECTLY is
# OFF then PLGIN_SOURCES and PLGIN_HEADERS are empty and we link
# against PLGIN_LIBRARY that is now the name of the target that
# builds the library.
#
# ============================================================================

find_package(GTest REQUIRED)
include_directories(${GTEST_INCLUDE_DIRS})

if (NOT INCLUDE_PILE_SOURCES_DIRECTLY)
    set (PLGIN_LIBRARY plgin)
endif()

add_executable(test_basic
    ${PLGIN_SOURCES}
    ${PLGIN_HEADERS}
    basic.cc)

target_link_libraries(test_basic
    ${GTEST_BOTH_LIBRARIES}
    ${PLGIN_LIBRARY})

add_test(
    NAME test_basic
    COMMAND $<TARGET_FILE:test_basic>)
