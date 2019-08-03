FROM naokitakahashi12/ros-vnc:melodic-desktop-full
RUN apt update && \
	apt upgrade -y && \
	apt install -y \
		apt-utils \
		git \
		python-catkin-pkg \
		python-rosdep \
		ros-melodic-catkin \
		python3-pip \
		python3-colcon-common-extensions \
		python3-setuptools \
		python3-vcstool \
	&& \
	pip3 install -U \
		setuptools \
	&& \
	wget http://bitbucket.org/eigen/eigen/get/3.3.7.tar.gz && \
	mkdir eigen && \
	tar --strip-components=1 -xzvf 3.3.7.tar.gz -C eigen && \
	mkdir eigen/build && \
	cd eigen/build && \
	cmake .. && \
	make install && \
	cd ../../ && \
	rm -rf 3.3.7.tar.gz eigen && \
	mkdir -p /autoware.ai/src && \
	cd /autoware.ai && \
	wget -O autoware.ai.repos "https://gitlab.com/autowarefoundation/autoware.ai/autoware/raw/1.12.0/autoware.ai.repos?inline=false" && \
	vcs import src < autoware.ai.repos && \
	bash -c ' \
        . /opt/ros/melodic/setup.bash; \
        rosdep init; \
        rosdep update; \
        rosdep install --from-paths src --ignore-src --rosdistro=melodic -y; \
		colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release; \
    ' && \ 
	apt autoremove -y && \
	apt clean && \
	rm -rf /var/lib/apt/lists/*
