# Maintainer: Augusto F. Hack <hack.augusto@gmail.com>
pkgname=diamond-git
pkgver=3.4
pkgrel=3
pkgdesc="Diamond is daemon that collects system metrics and publishes them to graphite and others"
arch=(any)
url="https://github.com/BrightcoveOS/Diamond"
license=('mit')
depends=('python2' 'python2-configobj')
makedepends=('git' 'python2' 'make' )
optdepends=('python2-psycopg2: Collect data from postgresql database')
backup=(etc/diamond/diamond.conf)
source=('diamond::git+https://github.com/BrightcoveOS/Diamond.git'
        'diamond.service')
md5sums=('SKIP'
         '65b275caf75c19e5040d3dbcd2a7e688')

pkgver() {
  cd "$srcdir/repo"
  git describe --long | sed -r 's/([^-]*-g)/r\1/;s/-/./g'
}

package() {
  cd "$srcdir/diamond"
  install -D -m644 $srcdir/diamond.service $pkgdir/usr/lib/systemd/system/diamond.service
  python2 setup.py install --root="$pkgdir/" --optimize=1
  rm $pkgdir/etc/diamond/diamond.conf.example.windows
  mv $pkgdir/etc/diamond/diamond.conf.example $pkgdir/etc/diamond/diamond.conf

  sed -i 's/collectors_reload_interval = 3600/collectors_reload_interval = 60/' $pkgdir/etc/diamond/diamond.conf

  mkdir -p $pkgdir/var/log/diamond $pkgdir/etc/diamond/collectors
}

# vim:set ts=2 sw=2 et:
