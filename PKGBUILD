# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://git.archlinux.org/svntogit/packages.git/log/trunk?h=packages/nghttp2
#						Maintainer: Anatol Pomozov
# 						Contributor: Zhuoyun Wei <wzyboy@wzyboy.org>

pkgname=nghttp2
pkgver=1.31.1
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
sha256sums=('65b9c83ae95a7760a14410aeefa9d441c34453027bc938df7a2272520f32e103')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

build() {
  cd nghttp2-$pkgver

  autoreconf -i
  ./configure \
    --prefix=/usr \
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
