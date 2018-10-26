# Contributor: Patrick Jackson <PatrickSJackson gmail com>
# Maintainer: Christoph Vigano <mail@cvigano.de>

pkgname=st
pkgver=0.8.1
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
url="http://st.suckless.org"
source=(http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz
        config.h
        https://st.suckless.org/patches/scrollback/st-scrollback-0.8.diff
        https://st.suckless.org/patches/scrollback/st-scrollback-mouse-0.8.diff
        #https://st.suckless.org/patches/alpha/st-alpha-0.8.1.diff
        https://st.suckless.org/patches/xresources/st-xresources-20180309-c5ba9c0.diff)
sha256sums=('SKIP'
            'SKIP'
            #'SKIP'
            'SKIP'
            'SKIP'
            'SKIP')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  # skip terminfo which conflicts with nsurses
  sed -i '/tic /d' Makefile
  cp $srcdir/config.h config.h
  #patches
  rm -f *.diff
  cp $srcdir/*.diff .
  patch -p1 -i st-scrollback-0.8.diff
  patch -p1 -i st-scrollback-mouse-0.8.diff
  #patch -p1 -i st-alpha-0.8.1.diff
  patch -p1 -i st-xresources-20180309-c5ba9c0.diff
}

build() {
  cd $srcdir/$pkgname-$pkgver
  #make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
  make
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
