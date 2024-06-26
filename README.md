# elevation_mapping_cpu

Simple package that contain all the dependencies for installing [elevation_mapping](https://github.com/ANYbotics/elevation_mapping) plus a docker image to use it.


## Installation

1. create a **new** ros workspace 
   ```sh
   mkdir -p ~/dls1_external_mapping/src
   ``` 

2. clone this repo inside **/src**  


3. clone the other submodules:

    `git submodule update --init --recursive`
    
4. build one of the dockerfile in the folder [installation/docker](https://github.com/giulioturrisi/elevation_mapping_cpu/tree/main/installation/docker)

    `docker build -t elevation_mapping_cpu_image .`


5. in your bashrc, put
    ```sh
    alias elevation_mapping_cpu_docker='
        if [ ! "$(docker ps -a -q -f name=elevation_mapping_cpu_container)" ]; then
            xhost + && docker run -it --rm -v /your_path_to/dls1_noetic/:/home/ -v /tmp/.X11-unix:/tmp/.X11-unix --device=/dev/input/ -e DISPLAY=$DISPLAY -e WAYLAND_DISPLAY=$WAYLAND_DISPLAY -e QT_X11_NO_MITSHM=1 --gpus all --net host --name elevation_mapping_cpu_container elevation_mapping_cpu_image; \
        else
            docker exec -it elevation_mapping_cpu_container bash; \
        fi'
    ```
where in **/your_path_to/dls1_noetic/** you can put the true path of the folder you created in step 1.


6. activate the docker container: 

    `elevation_mapping_cpu_docker`


7. compile it and run it!
    ```sh
    catkin_make
    run_elevation_mapping_cpu
    ```



