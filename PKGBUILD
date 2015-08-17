
pkgdesc="ROS - The pr2_mechanism_diagnostics node subscribes to mechanism_statistics and publishes diagnostics data for joints and controllers on /diagnostics."
url='http://www.ros.org/'

pkgname='ros-hydro-pr2-mechanism-diagnostics'
pkgver='1.8.11'
_pkgver_patch=0
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-hydro-diagnostic-msgs
  ros-hydro-pr2-mechanism-msgs
  ros-hydro-pr2-mechanism-model
  ros-hydro-roscpp
  ros-hydro-angles
  ros-hydro-catkin
  ros-hydro-diagnostic-updater
  ros-hydro-std-srvs
  ros-hydro-urdf
  ros-hydro-std-msgs
  ros-hydro-rostest)
makedepends=('cmake' 'git' 'ros-build-tools'
  ${ros_makedepends[@]})

ros_depends=(ros-hydro-diagnostic-msgs
  ros-hydro-rospy
  ros-hydro-pr2-mechanism-msgs
  ros-hydro-angles
  ros-hydro-diagnostic-updater
  ros-hydro-roscpp
  ros-hydro-pr2-mechanism-model
  ros-hydro-std-srvs
  ros-hydro-urdf
  ros-hydro-std-msgs)
depends=(${ros_depends[@]})

_tag=release/hydro/pr2_mechanism_diagnostics/${pkgver}-${_pkgver_patch}
_dir=pr2_mechanism_diagnostics
source=("${_dir}"::"git+https://github.com/ros-gbp/pr2_mechanism-release.git"#tag=${_tag})
md5sums=('SKIP')

build() {
  # Use ROS environment variables
  /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
