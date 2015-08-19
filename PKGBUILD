# Maintainer: Christof "chdorner" Dorner <https://github.com/chdorner>
pkgname=riemann
pkgver=0.2.10
pkgrel=2
pkgdesc="Monitors distributed systems"
arch=('any')
url="http://riemann.io/"
license=('EPL')
depends=('java-runtime' 'leiningen')
makedepends=('java-environment' 'git')
optdepends=('jdk: recommended jdk')
install='riemann.install'
source=(
  "git+https://github.com/aphyr/riemann.git#tag=$pkgver"
  riemann.service
  pkg.patch
  syslog.patch
)

backup=('etc/riemann/riemann.config')

prepare() {
  cd "$srcdir/$pkgname"

  patch -p0 < $srcdir/syslog.patch
  patch -p0 < $srcdir/pkg.patch
}

build() {
  cd "$srcdir/$pkgname"

  lein pkg
}

package() {
  cd "$srcdir/$pkgname"

  # creates the necessary dirs
  install -dm755 "$pkgdir/usr/share/riemann/bin"
  install -dm755 "$pkgdir/usr/share/riemann/lib"
  install -dm755 "$pkgdir/etc/riemann"
  install -dm755 "$pkgdir/var/lib/riemann"
  install -dm755 "$pkgdir/var/log/riemann"

  cp pkg/tar/riemann.config "$pkgdir/etc/riemann/"
  cp pkg/tar/riemann "$pkgdir/usr/share/riemann/bin"
  cp target/riemann-$pkgver-standalone.jar "$pkgdir/usr/share/riemann/lib/riemann.jar"

  # install systemd script
  install -Dm644 "$srcdir/riemann.service" "$pkgdir/usr/lib/systemd/system/riemann.service"
}
md5sums=('SKIP'
         'fb66da18a8186eff4fde4ea1890868f6'
         '5abf5c39282fe8eedf162e4996426e13'
         '8c247538e5ccfae0f6948d668751d8a8')
