# Maintainer: Joan Bruguera Micó <joanbrugueram@gmail.com>
# Contributor: Robin McCorkell <robin@mccorkell.me.uk>

_pkgname=cryptodev-linux
pkgbase=cryptodev-linux-comp-dkms-git
pkgname=cryptodev-linux-comp-dkms-git
pkgdesc="Kernel module providing access to Linux kernel cryptographic drivers from userspace - sources"
pkgver=r462.75a0944
pkgrel=2
url='http://cryptodev-linux.org/'
license=("GPL")
arch=('i686' 'x86_64' 'armv6h' 'armv7h')
depends=('dkms')
makedepends=('git')
conflicts=('cryptodev_friendly')
provides=('cryptodev_friendly')
optdepends=('openssl-cryptodev: OpenSSL with cryptodev support')
source=("$pkgbase::git+https://github.com/joanbm/cryptodev-linux-comp"
        "dkms.conf")
sha256sums=('SKIP'
            '4f48bef024e592b6fc0c44e2eda8231ce61750a293d1ef1bba99765ab3383b75')

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
