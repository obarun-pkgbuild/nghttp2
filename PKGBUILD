# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://git.archlinux.org/svntogit/packages.git/log/trunk?h=packages/nghttp2
#						Maintainer: Anatol Pomozov
# 						Contributor: Zhuoyun Wei <wzyboy@wzyboy.org>

pkgname=nghttp2
pkgver=1.28.0
pkgrel=2
pkgdesc='Framing layer of HTTP/2 is implemented as a reusable C library'
arch=(x86_64)
url='https://nghttp2.org/'
license=(MIT)
depends=('openssl' 'libev' 'zlib' 'libxml2' 'jansson' 'jemalloc' 'c-ares' 'libnghttp2')
options=(!emptydirs)
source=(https://github.com/nghttp2/nghttp2/releases/download/v$pkgver/nghttp2-$pkgver.tar.xz)
backup=(
  etc/nghttpx/nghttpx.conf
  etc/logrotate.d/nghttpx
)
sha256sums=('0d6c3f00614deca3935e42a27f6ad0ea87c31d8c1baa3a9c52755955c599fd8d')

build() {
  cd nghttp2-$pkgver

  autoreconf -i
  ./configure \
    --prefix=/usr \
    --with-spdylay=no \
    --disable-examples \
    --disable-python-bindings \
    --without-systemd
  make
}

check() {
  cd nghttp2-$pkgver
  make check
}

package() {
  cd nghttp2-$pkgver

  make DESTDIR="$pkgdir" install
  make -C lib DESTDIR="$pkgdir" uninstall

 # install -Dm644 contrib/nghttpx.service "$pkgdir/usr/lib/systemd/system/nghttpx.service"
  install -Dm644 contrib/nghttpx-logrotate "$pkgdir/etc/logrotate.d/nghttpx"
  install -Dm644 nghttpx.conf.sample "$pkgdir/etc/nghttpx/nghttpx.conf"
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/nghttp2/COPYING"
}
