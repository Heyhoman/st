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
	st-scrollback-20201205-4ef0cbd.diff
	st-anysize-0.8.1.diff
	st-hidecursor-0.8.3.diff
	st-no_bold_colors-20170623-b331da5.diff
	config.h)
sha256sums=('d42d3ceceb4d6a65e32e90a5336e3d446db612c3fbd9ebc1780bc6c9a03346a6'
            '3b8c7d1815352cbfa2e100f6bb65e4c7d5a338952a6e7513b59a6a6297f32fb4'
            '8118dbc50d2fe07ae10958c65366476d5992684a87a431f7ee772e27d5dee50f'
            '31bb2d8f2a297ec8854d990cc923f813604e3cbc3265432e0078b73b2e5614dd'
            '71e1211189d9e11da93ee49388379c5f8469fcd3e1f48bb4d791ddaf161f5845'
            '09937fb2af0fbcc92356f76f9b2e1f73a8613946d1811f263644ffab884849b4')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h
  sed -i '/tic -sx st.info/d' Makefile

  for patch in $srcdir/*.diff; do
    if [ -f $patch ]; then
      echo "Applying $(basename $patch)"
      patch -p1 --quiet < $patch
    fi
  done
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
