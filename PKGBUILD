# Maintainer: Tray Torrance

pkgname=taskd
pkgver=1.0.0
pkgrel=1
pkgdesc="TaskWarrior's TaskServer"
arch=('i686' 'x86_64')
url='http://taskwarrior.org/download/taskd-1.0.0.tar.gz'
license=('MIT')
depends=('gnutls' 'libutil-linux' 'readline')
makedepends=('cmake' 'make' 'gcc')
install=taskd.install
source=(
'http://taskwarrior.org/download/taskd-1.0.0.tar.gz'
'taskd.service')
sha1sums=(
'5a89406a21be1f95ece03674315b35814fe4f037'
'0969635d438dd9aab662a7debcdc99cbd658fedf')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  cmake -DCMAKE_INSTALL_PREFIX=/usr .
  make
}

package() {
  install -o 47   -g 47   -m 0755 -d "${pkgdir}/var/lib/taskd"
  install -o root -g root -m 0755 -d "${pkgdir}/usr/share/taskd"
  install -o 47   -g root -m 0755 -d "${pkgdir}/usr/share/taskd/pki"
  install -o root -g root -m 0755 -d "${pkgdir}/usr/lib/systemd/system"
  install -o root -g root -m 0644 "${pkgname}.service" "${pkgdir}/usr/lib/systemd/system"

  find "${srcdir}/${pkgname}-${pkgver}/pki" \
    -exec install -o 47 -g root -m 0750     \
    -t "${pkgdir}/usr/share/taskd/pki"      \
    {} \;

  make -C "${srcdir}/${pkgname}-${pkgver}" DESTDIR="$pkgdir" install
}
