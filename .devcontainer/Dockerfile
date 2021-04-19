FROM athackst/ros:melodic-gazebo

# ** [Optional] Uncomment this section to install additional packages. **
#
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
   && apt-get -y install --no-install-recommends \
   python-catkin-tools \
   && apt-get autoremove -y \
   && apt-get clean -y \
   && rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=dialog


################
# Expose the nvidia driver to allow opengl 
# Dependencies for glvnd and X11.
################
RUN apt-get update \
 && apt-get install -y -qq --no-install-recommends \
  libxau6 \
  libglvnd0 \
  libgl1 \
  libglx0 \
  libegl1 \
  libxext6 \
  libx11-6 \
  && apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*

ENV DEBIAN_FRONTEND=dialog

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES \
    ${NVIDIA_VISIBLE_DEVICES:-all}
ENV NVIDIA_DRIVER_CAPABILITIES \
    ${NVIDIA_DRIVER_CAPABILITIES:+$NVIDIA_DRIVER_CAPABILITIES,}graphics,utility,compute
ENV QT_X11_NO_MITSHM 1


# Set up auto-source of workspace for ros user
ARG WORKSPACE
RUN echo "if [ -f ${WORKSPACE}/devel/setup.bash ]; then source ${WORKSPACE}/devel/setup.bash; fi" >> /home/ros/.bashrc
