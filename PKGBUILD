# Maintainer: George Brooke <george+arch.aur@george-brooke.co.uk>
# Contributor: Adria Arrufat <swiftscythe@gmail.com>

pkgname=telepathy-kde-kded-module-git
pkgver=20111226
pkgrel=1
pkgdesc="A module that sits in KDED and takes care of various bits of system integration like setting user to auto-away or handling connection errors."
arch=('i686' 'x86_64')
url="https://projects.kde.org/projects/kdereview/ktp-kded-module"
license=("GPL")
depends=('telepathy-kde-common-internals-git')
makedepends=('git' 'cmake' 'automoc4')

_gitroot="git://anongit.kde.org/ktp-kded-module"
_gitname="ktp-kded-module"


build() {
  cd ${srcdir}
  msg "Connecting to GIT server...."

  if [ -d "${srcdir}/$_gitname" ] ; then
    cd $_gitname
    git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf ${srcdir}/build
  mkdir -p ${srcdir}/build
  cd ${srcdir}/build

  cmake ../$_gitname \
  -DCMAKE_INSTALL_PREFIX=$( kde4-config --prefix )
  
  make
}

package(){
  cd ${srcdir}/build
  make DESTDIR=${pkgdir} install 

}
