
pkgname=skeltrack-git
pkgver=20120405
pkgrel=1
pkgdesc="A Free Software skeleton tracking library"
arch=('i686' 'x86_64')
url="https://github.com/joaquimrocha/Skeltrack-Desktop-Control"
license=('GPL3')
depends=('gobject-introspection')
makedepends=('git' 'make' 'gtk-doc')

_gitroot="git://github.com/joaquimrocha/Skeltrack.git"
_gitname="skeltrack"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone -l "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"
  ./autogen.sh
  ./configure --prefix=/usr
  make 
} 

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR=${pkgdir} install
  rm -rf "$srcdir/$_gitname-build"
}
