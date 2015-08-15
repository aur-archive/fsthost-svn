# Maintainer: rtfreedman  (rob<d0t>til<d0t>freedman<aT>googlemail<d0t>com

pkgname=fsthost-svn
_svnmod=fsthost
pkgver=401
pkgrel=1
url="http://sourceforge.net/projects/fsthost/"
pkgdesc="A linux VST host using winelib, fork of FreeST."
license=('GPL')
#
arch=('i686' 'x86_64')
install="$pkgname.install"
depends=('libxml2' 'lash' 'gtk3')
#[[ "$CARCH" = 'x86_64' ]] && _arch=32 && depends=(${depends[@]/#/lib32-})
depends+=('wine' 'jack')
makedepends=('subversion')
optdepends=('perl-xml-libxml: for fsthost_menu.pl')
conflicts=('fsthost')
source=("$_svnmod::svn+http://svn.code.sf.net/p/fsthost/code/trunk")
md5sums=('SKIP')


pkgver() {
  cd "$_svnmod"
  svnversion | tr -d [A-z]
}

build() {
  cd "$_svnmod"

# default GTK3: make
# force   GTK2: make GTK=2
# without GTK : make GTK=0 
# without lash: make LASH_EXISTS=no
# force  arch : make PLAT=32 resp. make PLAT=64
# missing lash cflags
  export CFLAGS+=" $(pkg-config --cflags lash-1.0)"
  make
}

#	LIB64_INST_PATH=/usr/lib LIB32_INST_PATH=/usr/lib$_arch 

package() {
  cd "$_svnmod"
  make PREFIX=/usr \
  DESTDIR="$pkgdir" \
  MANDIR=/usr/share/man/man1 install
  # add minimal docs
  install -Dm644 README "$pkgdir"/usr/share/doc/$pkgname/README
}
