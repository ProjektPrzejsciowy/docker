FROM ros:kinetic-ros-base

# setup keys
RUN apt-key adv --keyserver ha.pool.sks-keyservers.net --recv-keys D2486D2DD83DB69272AFE98867170598AF249743

# setup sources.list
RUN echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-stable `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-latest.list

# install Gazebo
RUN apt-get update && apt-get install -q -y \
    gazebo7 \
    && rm -rf /var/lib/apt/lists/*

# install ROS packages for interfacing with Gazebo
RUN apt-get update
RUN apt-get install -y ros-kinetic-gazebo-ros-pkgs ros-kinetic-gazebo-ros-control

# setup gazebo plugin
RUN /bin/bash -c "source /opt/ros/kinetic/setup.bash ;\
                  mkdir -p ~/catkin_ws/src ;\
                  cd ~/catkin_ws/src ;\
                  catkin_init_workspace ;\
                  git clone https://github.com/ProjektPrzejsciowy/projekt_przejsciowy.git ;\
                  cd ~/catkin_ws/ ;\
                  catkin_make ;\
                  rm -rf ./src/projekt_przejsciowy/src ;\
                  rm ./src/projekt_przejsciowy/README.md"

# setup required models for Gazebo
RUN /bin/bash -c "mkdir -p ~/.gazebo ;\
                  cd ~/.gazebo ;\
                  git clone https://github.com/ProjektPrzejsciowy/models.git ;\
                  rm -rf ./models/.git"

# path and source config
RUN /bin/bash -c "echo 'export GAZEBO_PLUGIN_PATH='/root/catkin_ws/devel/lib/'' >> ~/.bashrc ;\
                  echo 'source ~/catkin_ws/devel/setup.bash' >> ~/.bashrc"


