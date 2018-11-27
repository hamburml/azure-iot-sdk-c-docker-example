cmake_minimum_required(VERSION 2.8.11)
project(example_project)

# The demonstration uses C99 but it could just as easily be a C++ application
set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")

set(iothub_c_files
    prov_dev_client_ll_sample.c
)

# Set up the include and library paths
include_directories(/root/gcc-linaro-7.3.1-2018.05-x86_64_arm-linux-gnueabihf/usr/include/azureiot;
                    /root/gcc-linaro-7.3.1-2018.05-x86_64_arm-linux-gnueabihf/usr/include)
link_directories(/root/gcc-linaro-7.3.1-2018.05-x86_64_arm-linux-gnueabihf/usr/lib)

add_executable(example ${iothub_c_files})

# Redundant in this case but shows how to rename your output executable
set_target_properties(example PROPERTIES OUTPUT_NAME "example") 

# List the libraries required by the link step
target_link_libraries(example iothub_client prov_auth_client hsm_security_client prov_device_ll_client prov_http_transport aziotsharedutil iothub_client_mqtt_transport umqtt ssl crypto curl pthread parson m)
