# Maintainer: Eric Bélanger <eric@archlinux.org>

pkgname=racket
pkgver=6.1.1
pkgrel=1
pkgdesc="A programming language environment (formerly known as PLT Scheme) suitable for tasks ranging from scripting to application development"
arch=('i686' 'x86_64')
url="http://racket-lang.org/"
license=('GPL3' 'LGPL3' 'custom')
depends=('gtk2')
makedepends=('gsfonts' 'sqlite')
options=('!strip' '!emptydirs')
install=racket.install
source=(http://download.racket-lang.org/installers/${pkgver}/${pkgname}-${pkgver}-src.tgz)
sha1sums=('be04ed6e444fbb412e48e06a62da3a9eba993b44')

prepare() {
  echo "Icon=drracket" >> ${pkgname}-${pkgver}/share/pkgs/drracket/drracket/drracket.desktop
}

build() {
  cd ${pkgname}-${pkgver}/src
  [ "$CARCH" == "x86_64" ] && export CFLAGS+=" -fPIC"
  ./configure --prefix=/usr --sysconfdir=/etc --enable-shared
  make
}

package() {
  cd ${pkgname}-${pkgver}/src
  make DESTDIR="${pkgdir}" install
  install -D -m644 COPYING-libscheme.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

  install -D -m644 ../share/pkgs/drracket/drracket/drracket.desktop "${pkgdir}/usr/share/applications/drracket.desktop"
  install -d "${pkgdir}"/usr/share/icons/hicolor/{16x16,32x32,48x48,256x256}/apps
  ln -s /usr/share/racket/pkgs/icons/plt-16x16.png "${pkgdir}/usr/share/icons/hicolor/16x16/apps/drracket.png"
  ln -s /usr/share/racket/pkgs/icons/plt-32x32.png "${pkgdir}/usr/share/icons/hicolor/32x32/apps/drracket.png"
  ln -s /usr/share/racket/pkgs/icons/plt-48x48.png "${pkgdir}/usr/share/icons/hicolor/48x48/apps/drracket.png"
  ln -s /usr/share/racket/pkgs/icons/plt-logo-red-diffuse.png "${pkgdir}/usr/share/icons/hicolor/256x256/apps/drracket.png"
}
