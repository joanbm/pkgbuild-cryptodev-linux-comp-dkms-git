# Maintainer: Joan Bruguera Micó <joanbrugueram@gmail.com>
# Contributor: Robin McCorkell <robin@mccorkell.me.uk>

_pkgname=cryptodev-linux-comp
_pkgbase=cryptodev
pkgname=${_pkgname}-dkms-git
pkgver=r379.45ba871
pkgrel=1
pkgdesc="cryptodev Linux module (with compression support)"
url='http://cryptodev-linux.org/'
license=("GPL")
arch=('i686' 'x86_64' 'armv6h' 'armv7h')
depends=('dkms')
conflicts=('cryptodev_friendly')
provides=('cryptodev_friendly')
optdepends=('openssl-cryptodev: OpenSSL with cryptodev support')
source=('cryptodev-linux-comp::git+https://github.com/joanbm/cryptodev-linux'
        'dkms.conf')
sha256sums=('SKIP'
            '4a9a5ab58299faa3d4c4d0f9fbfd1999e870d0a8e1288640d6a1bf8235507266')

pkgver() {
  cd "${srcdir}/${_pkgname}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

package() {
  cd "${srcdir}/${_pkgname}"
  install -d "${pkgdir}/usr/src/${_pkgname}-${pkgver}/"
  cp -r "${srcdir}/${_pkgname}/"* "${pkgdir}/usr/src/${_pkgname}-${pkgver}/"

  install -Dm644 "${srcdir}/dkms.conf" "${pkgdir}/usr/src/${_pkgname}-${pkgver}/dkms.conf"
  sed -e "s/@_PKGNAME@/${_pkgname}/" \
    -e "s/@_PKGBASE@/${_pkgbase}/" \
    -e "s/@PKGVER@/${pkgver}/" \
    -i "${pkgdir}/usr/src/${_pkgname}-${pkgver}/dkms.conf"

  install -Dm644 "crypto/cryptodev.h" "${pkgdir}/usr/include/crypto/cryptodev.h"
}
