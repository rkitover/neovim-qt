
include_directories(${CMAKE_SOURCE_DIR}/src)

add_custom_target(check COMMAND ${CMAKE_CTEST_COMMAND})
function(add_xtest SOURCE_NAME)
	add_executable(${SOURCE_NAME} ${SOURCE_NAME}.cpp ${ARGV1})
	target_link_libraries(${SOURCE_NAME} Qt5::Network Qt5::Test ${MSGPACK_LIBRARIES} neovim-qt)
	add_test(NAME ${SOURCE_NAME} COMMAND ${SOURCE_NAME})
	add_dependencies(check ${SOURCE_NAME})
endfunction()

add_xtest(tst_neovimobject)
add_xtest(tst_neovimconnector)
add_xtest(tst_callallmethods)
add_xtest(tst_encoding)
add_xtest(tst_msgpackiodevice)
add_xtest(tst_input ${CMAKE_SOURCE_DIR}/src/gui/input.cpp)
