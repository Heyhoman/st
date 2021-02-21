pkgname=st
pkgver=0.8.4
pkgrel=1
pkgdesc="A simple virtual terminal emulator for X"
arch=('i686' 'x86_64')
url="http://st.suckless.org"
license=('MIT')
depends=('libxft' 'ttf-hack')
provides=('st')
conflicts=('st')
options=(zipman)
source=(https://dl.suckless.org/$pkgname/$pkgname-$pkgver.tar.gz
	config.h)
sha256sums=('d42d3ceceb4d6a65e32e90a5336e3d446db612c3fbd9ebc1780bc6c9a03346a6'
            '0afb43605ac03bb4fd92c7bc38efa1d053db75e2513e135d3334f6c230a2cde3')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h
  sed -i '/tic -sx st.info/d' Makefile
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
}
