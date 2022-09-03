pkgname=st
pkgver=0.8.5
pkgrel=1
pkgdesc="A simple virtual terminal for X"
url="https://st.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libxft' 'ttf-hack')
source=(https://dl.suckless.org/st/st-$pkgver.tar.gz
        config.h)
sha256sums=('ea6832203ed02ff74182bcb8adaa9ec454c8f989e79232cb859665e2f544ab37'
            '00c9e6e79b84e8ee80ad4baeac915628973548c70ef349c0d42419b0f90c3077')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h

  for patch in "$srcdir"/*.diff; do
    if [ -f "$patch" ]; then
      echo "Applying $(basename "$patch")"
      patch -p1 --quiet < "$patch"
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
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
