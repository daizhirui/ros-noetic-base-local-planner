pkgdesc="ROS - This package provides implementations of the Trajectory Rollout and Dynamic Window approaches to local robot navigation on a plane."
url='https://wiki.ros.org/base_local_planner'

pkgname='ros-noetic-base-local-planner'
pkgver='1.17.3'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
pkgrel=1
license=('BSD')

ros_makedepends=(
    ros-noetic-catkin
    ros-noetic-cmake-modules
    ros-noetic-message-generation
    ros-noetic-tf2-geometry-msgs
)

makedepends=(
    cmake
    ros-build-tools
    ${ros_makedepends[@]}
)

ros_depends=(
    ros-noetic-angles
    ros-noetic-costmap-2d
    ros-noetic-dynamic-reconfigure
    ros-noetic-geometry-msgs
    ros-noetic-nav-core
    ros-noetic-nav-msgs
    ros-noetic-pluginlib
    ros-noetic-sensor-msgs
    ros-noetic-std-msgs
    ros-noetic-rosconsole
    ros-noetic-roscpp
    ros-noetic-rospy
    ros-noetic-tf2
    ros-noetic-tf2-ros
    ros-noetic-visualization-msgs
    ros-noetic-voxel-grid
    ros-noetic-message-runtime
)

depends=(
    ${ros_depends[@]}
    eigen
)

_dir="navigation-${pkgver}/base_local_planner"
source=("${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-planning/navigation/archive/${pkgver}.tar.gz")
sha256sums=('6500e427f868ea63801203715f41cbec4ed1bd1f9a29ae130a74b3776a7684f6')

build() {
  # Use ROS environment variables
  source /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
