# FROM osrf/ros:humble-desktop
FROM nvidia/cuda:12.6.3-cudnn-devel-ubuntu24.04
LABEL maintainer="Ryohei Kobayashi <kobayashi.ryohei621@mail.kyutech.jp>"

SHELL ["/bin/bash", "-c"]
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    git \
    wget \
    vim \
    lsb-release \
    build-essential \
    cmake \
    libgl1 \
    libglib2.0-0 \
    python3.12-venv \
    python3-pip \
    # python3-colcon-common-extensions \
    # python3-rosdep \
    # python3-pip \
    # ros-humble-pcl-ros \
    # ros-humble-tf2-ros \
    # ros-humble-tf2-eigen \
    # ros-humble-tf2-sensor-msgs \
    # ros-humble-pcl-conversions \
    # ros-humble-velodyne-driver \
    # ros-humble-velodyne-pointcloud \
    # ros-humble-pointcloud-to-laserscan \
    # ros-humble-rmw-cyclonedds-cpp \
    # wireshark \
    # nmap \
    && rm -rf /var/lib/apt/lists/*

# from python3.12, requires to setup pythonenv by venv
RUN python3 -m venv /my_env
ENV PATH="/my_env/bin:$PATH"

RUN pip install --upgrade pip
RUN pip install torch torchvision --index-url https://download.pytorch.org/whl/cu126
RUN pip install numpy==1.26.4 \
                 pandas \
                 scikit-learn \
                 matplotlib \
                 pillow \
                 opencv-python \
                 deepdish \
                 h5py 



# RUN rosdep update

# WORKDIR /ros2_ws/src
# RUN rosdep install --from-paths . --ignore-src -r -y

WORKDIR /grasping-state-assessment

COPY ./../grasping-state-assessment ./grasping-state-assessment


# RUN cd /ros2_ws && \
#     . /opt/ros/humble/setup.sh && \
#     colcon build --symlink-install
# 
# RUN . /opt/ros/humble/setup.sh && \
#     . /ros2_ws/install/setup.sh
# 
# 
# COPY ./assets/cyclonedds_profile.xml /ros2_ws/cyclonedds_profile.xml

COPY ./assets/entrypoint.sh /ros_entrypoint.sh
RUN chmod +x /ros_entrypoint.sh
ENTRYPOINT [ "/ros_entrypoint.sh" ]

WORKDIR /grasping-state-assessment

