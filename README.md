# elevation_mapping_cpu

Simple package that contain all the dependencies for installing [elevation_mapping](https://github.com/ANYbotics/elevation_mapping) with mamba.


## Installation

1. create a **new** ros workspace 
   ```sh
   mkdir -p ~/dls1_noetic/src
   ``` 

2. clone this repo inside /src  

3. install [miniforge](https://github.com/conda-forge/miniforge/releases) (x86_64)

4. create an environment using the file in the folder [installation](https://github.com/iit-DLSLab/Quadruped-PyMPC/tree/main/installation):

    `conda env create -f mamba_environment.yml`


5. clone the other submodules:

    `git submodule update --init --recursive`
    
6. activate the conda environment

    `conda activate elevation_mapping_cpu_env`


7. run:
    ```sh
    # this adds the conda-forge channel to the new created environment configuration 
    conda config --env --add channels conda-forge
    # and the robostack channel
    conda config --env --add channels robostack-staging
    # remove the defaults channel just in case, this might return an error if it is not in the list which is ok
    conda config --env --remove channels defaults
    # install ros noetic
    mamba install ros-noetic-desktop
    mamba install ros-noetic-navigation
    mamba install ros-noetic-pcl-ros
    mamba install ros-noetic-octomap-ros
    ```

8. see this [commit](https://github.com/ANYbotics/grid_map/commit/8a95e563ee3c5e9673217c103c5165aa6fb73275) to modify something inside grid_map



9. compile with
    ```sh
    catkin_make
    ```



