# Maintainer: Joan Bruguera Micó <joanbrugueram@gmail.com>
# Contributor: Robin McCorkell <robin@mccorkell.me.uk>

_pkgname=cryptodev-linux
pkgbase=cryptodev-linux-comp-dkms-git
pkgname=cryptodev-linux-comp-dkms-git
pkgdesc="Kernel module providing access to Linux kernel cryptographic drivers from userspace - sources"
pkgver=r450.f0a98bc
pkgrel=1
url='http://cryptodev-linux.org/'
license=("GPL")
arch=('i686' 'x86_64' 'armv6h' 'armv7h')
depends=('dkms')
conflicts=('cryptodev_friendly')
provides=('cryptodev_friendly')
optdepends=('openssl-cryptodev: OpenSSL with cryptodev support')
source=("$pkgbase::git+https://github.com/joanbm/cryptodev-linux-comp"
        "dkms.conf")
sha256sums=('SKIP'
            '4c762bbea27edeb283d44af37be2faf2df21312853b200e6b93319d563f51d86')

pkgver() {
  cd "${srcdir}/${pkgbase}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
  cd "${srcdir}/${pkgbase}"
  install -d "${pkgdir}/usr/src/${_pkgname}-${pkgver}/"
  cp -r ./* "${pkgdir}/usr/src/${_pkgname}-${pkgver}/"

  install -Dm644 "${srcdir}/dkms.conf" "${pkgdir}/usr/src/${_pkgname}-${pkgver}/dkms.conf"
  sed -e "s/@PKGBASE@/${_pkgname}/" \
    -e "s/@PKGVER@/${pkgver}/" \
    -i "${pkgdir}/usr/src/${_pkgname}-${pkgver}/dkms.conf"

  install -Dm644 "crypto/cryptodev.h" "${pkgdir}/usr/include/crypto/cryptodev.h"
}
