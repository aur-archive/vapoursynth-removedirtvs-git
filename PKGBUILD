# Maintainer:  Gustavo Alvarez <sl1pkn07@gmail.com>

_plug=removedirtvs
pkgname=vapoursynth-${_plug}-git
pkgver=20131120.ddc78e5
pkgrel=1
pkgdesc="Plugin for Vapoursynth: ${_plug} (GIT version)"
arch=('i686' 'x86_64')
url="https://github.com/handaimaoh/${_plug}"
license=('GPL')
depends=('vapoursynth')
provides=("vapoursynth-${_plug}")
conflicts=("vapoursynth-${_plug}" "vapoursynth-plugin-${_plug}")
makedepends=('git')
source=("${_plug}::git+https://github.com/handaimaoh/${_plug}.git"
        'README'
        'removedirtvs.py')
md5sums=('SKIP'
         'fa29223bedb9fa955f7016c2af351f1e'
         '3c110b86f8b99f08554e635ff503d515')
_gitname="${_plug}"

pkgver() {
  cd "${_gitname}"
  echo "$(git log -1 --format="%cd" --date=short | tr -d '-').$(git log -1 --format="%h")"
}

prepare() {
  cd "${_gitname}"
  echo "all:
	  g++ -shared -fPIC -fpermissive -DVS_TARGET_CPU_X86=1 -I. -o ${_plug}.so *.cpp " > Makefile
}

build() {
  cd "${_gitname}"
  make
}

package(){
  cd "${_gitname}"
  install -Dm755 "${_plug}.so" "${pkgdir}/usr/lib/vapoursynth/${_plug}.so"
  install -Dm644 "${srcdir}/removedirtvs.py" "${pkgdir}/usr/lib/python3.3/site-packages/removedirtvs.py"
  install -Dm644 "${srcdir}/README" "${pkgdir}/usr/share/doc/vapoursynth/plugins/${_plug}/README"
}
