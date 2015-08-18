# Maintainer: Christof "chdorner" Dorner <https://github.com/chdorner>
pkgname=riemann
pkgver=0.2.10
pkgrel=1
pkgdesc="Monitors distributed systems"
arch=('any')
url="http://riemann.io/"
license=('EPL')
depends=('java-runtime' 'bash')
install='riemann.install'
source=(
  "http://aphyr.com/riemann/$pkgname-$pkgver.tar.bz2"
  riemann.service
)

backup=('etc/riemann/riemann.config')

build() {
  cd "$srcdir/$pkgname-$pkgver"
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  # creates the necessary dirs
  install -dm755 "$pkgdir/usr/share/riemann/bin"
  install -dm755 "$pkgdir/etc/riemann"
  install -dm755 "$pkgdir/var/lib/riemann"
  install -dm755 "$pkgdir/var/log/riemann"

  cp etc/* "$pkgdir/etc/riemann/"
  cp -r {bin,lib}   "$pkgdir/usr/share/riemann"

  # install systemd script
  install -Dm644 "$srcdir/riemann.service" "$pkgdir/usr/lib/systemd/system/riemann.service"
}
md5sums=('c15e245a0658b9f1fe56137f523af59a'
         'fb66da18a8186eff4fde4ea1890868f6')
