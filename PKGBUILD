# Maintainer: Robin McCorkell <robin@mccorkell.me.uk>
# Contributor: Joan Bruguera Micó <joanbrugueram@gmail.com>

_pkgname=cryptodev-linux-comp
pkgname=${_pkgname}-git
pkgver=r375.02931ca
pkgrel=1
pkgdesc="cryptodev Linux module"
url='http://cryptodev-linux.org/'
license=("GPL")
arch=('i686' 'x86_64' 'armv6h' 'armv7h')
makedepends=('linux-headers')
conflicts=('cryptodev_friendly')
provides=('cryptodev_friendly')
optdepends=('openssl-cryptodev: OpenSSL with cryptodev support')
source=('cryptodev-linux-comp::git+https://github.com/plauth/cryptodev-linux')
sha256sums=('SKIP')
install=${_pkgname}.install

pkgver() {
  cd "${srcdir}/${_pkgname}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "${srcdir}/${_pkgname}"
  make
}

package() {
  cd "${srcdir}/${_pkgname}"
  make INSTALL_MOD_PATH=${pkgdir}/usr DESTDIR=${pkgdir} PREFIX=${pkgdir} install
  rm -Rf "${pkgdir}"/usr/lib/modules/*/modules.*
}
