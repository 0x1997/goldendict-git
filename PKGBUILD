# Maintainer: Zhe Wang <0x1998@gmail.com>
pkgname=goldendict-git
pkgver=1.5.0.RC.640.gb662227
pkgrel=1
pkgdesc="Feature-rich dictionary lookup program."
arch=('i686' 'x86_64')
url="http://goldendict.org/"
license=('GPL3')
depends=('ffmpeg' 'hunspell' 'libao' 'libeb' 'libvorbis' 'libxtst' 'lzo2'
         'qt5-base' 'qt5-svg' 'qt5-tools' 'qt5-webkit' 'qt5-x11extras' 'zlib'
         'xz' 'opencc')
makedepends=('git')
conflicts=('goldendict' 'goldendict-svn' 'goldendict-git-opt')
provides=('goldendict')
replaces=('goldendict' 'goldendict-svn' 'goldendict-git-opt')
_gitname="goldendict"
source=(git://github.com/0x1997/goldendict.git)
sha256sums=(SKIP)

pkgver() {
  cd ${_gitname}
  git describe --always | sed 's|-|.|g'
}

prepare() {
  cd ${_gitname}
  msg "Fixing flags"
  echo "QMAKE_CXXFLAGS_RELEASE = $CFLAGS" >> goldendict.pro
  echo "QMAKE_CFLAGS_RELEASE = $CXXFLAGS" >> goldendict.pro
}

build(){
  cd ${_gitname}
  PREFIX="/usr" qmake-qt5 "CONFIG+=chinese_conversion_support" "CONFIG+=zim_support"
  make
}

package() {
  cd ${_gitname}
  make INSTALL_ROOT="${pkgdir}" install
}
