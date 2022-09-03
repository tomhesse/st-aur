pkgname=st
pkgver=0.8.5
pkgrel=5
pkgdesc="A simple virtual terminal for X"
url="https://st.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libxft' 'ttf-hack')
source=(https://dl.suckless.org/st/st-$pkgver.tar.gz
        https://st.suckless.org/patches/scrollback/st-scrollback-ringbuffer-0.8.5.diff
        https://st.suckless.org/patches/anysize/st-anysize-20220718-baa9357.diff
        https://st.suckless.org/patches/hidecursor/st-hidecursor-0.8.3.diff
        config.h)
sha256sums=('ea6832203ed02ff74182bcb8adaa9ec454c8f989e79232cb859665e2f544ab37'
            'b054f3c4b5a076645aecd927658ae7027a0c4b859cbd0b9a42fab07fdf7cbc77'
            '78ef0c10f45bdee6824ed0739c6f8b6a88d7aa5723e1e4f8db6ad0829c68a5fa'
            '31bb2d8f2a297ec8854d990cc923f813604e3cbc3265432e0078b73b2e5614dd'
            'bc7f37f6152fc096be83d263a7d2af8311f5beb6a004bafd4199beb75a5bc154')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h

  # Don't compile terminfo
  sed -i '/tic -sx st.info/d' Makefile

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
