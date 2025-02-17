cmake_minimum_required(VERSION 3.5)


add_compile_options(-fPIC)



#test routing
add_executable(test_routing 
                    ${CMAKE_CURRENT_SOURCE_DIR}/test_routing.cc)
target_link_libraries(test_routing PUBLIC
        gtest
        gtest_main
        apollo_routing
)


add_executable(test_talker talker.cc
                        ./../cyber/examples/proto/examples.pb.cc)
target_link_libraries(test_talker cyber apollo
${TORCH_LIBRARIES})

add_executable(test_listener listener.cc
                                ./../cyber/examples/proto/examples.pb.cc)
target_link_libraries(test_listener cyber)


add_executable(test_talker_null test_publish_null_msg.cc
                        ./../cyber/examples/proto/examples.pb.cc)
target_link_libraries(test_talker_null cyber
apollo
${TORCH_LIBRARIES})

add_executable(test_listener_null test_subscribe_null_msg.cc
                                ./../cyber/examples/proto/examples.pb.cc)
target_link_libraries(test_listener_null cyber)


install(
        TARGETS 
                test_routing
                test_talker
                test_listener
                test_talker_null
                test_listener_null
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}
)

