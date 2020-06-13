

# Maintainer: Joan Bruguera Micó <joanbrugueram@gmail.com>
# Contributor: Robin McCorkell <robin@mccorkell.me.uk>

_pkgbase=cryptodev-linux
pkgbase=cryptodev-linux-comp-git
pkgname=(cryptodev-linux-comp-git cryptodev-linux-comp-dkms-git)
pkgdesc="Kernel module providing access to Linux kernel cryptographic drivers from userspace"
pkgver=r404.ec5829f
pkgrel=2
url='http://cryptodev-linux.org/'
license=("GPL")
arch=('i686' 'x86_64' 'armv6h' 'armv7h')
makedepends=('linux-headers')
conflicts=('cryptodev_friendly')
provides=('cryptodev_friendly')
optdepends=('openssl-cryptodev: OpenSSL with cryptodev support')
source=("$pkgbase::git+https://github.com/joanbm/cryptodev-linux"
        "0001-Fix-build-for-Linux-5.8.patch"
        "dkms.conf")
sha256sums=('SKIP'
            'a412cbbece30d34886cdb13921f82e67030ccaa14bc2e8d88b7110028a300c8b'
            '4c762bbea27edeb283d44af37be2faf2df21312853b200e6b93319d563f51d86')
install=${_pkgbase}.install

pkgver() {
  cd "${srcdir}/${pkgbase}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd "${srcdir}/${pkgbase}"
  patch -Np1 -i "${srcdir}/0001-Fix-build-for-Linux-5.8.patch"
}

build() {
  cd "${srcdir}/${pkgbase}"
  make KERNEL_DIR=/usr/src/linux
}

package_cryptodev-linux-comp-git() {
  depends=('linux')

  cd "${srcdir}/${pkgbase}"
  make INSTALL_MOD_PATH="${pkgdir}"/usr DESTDIR="${pkgdir}" PREFIX="${pkgdir}" KERNEL_DIR=/usr/src/linux install
  rm -Rf "${pkgdir}"/usr/lib/modules/*/modules.*
}

package_cryptodev-linux-comp-dkms-git() {
  pkgdesc+=" - sources"
  depends=('dkms')

  cd "${srcdir}/${pkgbase}"
  install -d "${pkgdir}/usr/src/${pkgbase}-${pkgver}/"
  cp -r ./* "${pkgdir}/usr/src/${pkgbase}-${pkgver}/"

  # TODO: Is there some better way to avoid copying the files created
  #       during the build process to the DKMS folder?
  find "${pkgdir}/usr/src/${pkgbase}-${pkgver}/" -name "*.o" -type f -delete
  rm -f "${pkgdir}/usr/src/${pkgbase}-${pkgver}/Module.symvers"
  rm -f "${pkgdir}/usr/src/${pkgbase}-${pkgver}/cryptodev.ko"
  rm -f "${pkgdir}/usr/src/${pkgbase}-${pkgver}/cryptodev.mod"
  rm -f "${pkgdir}/usr/src/${pkgbase}-${pkgver}/cryptodev.mod.c"
  rm -f "${pkgdir}/usr/src/${pkgbase}-${pkgver}/modules.order"
  rm -f "${pkgdir}/usr/src/${pkgbase}-${pkgver}/version.h"

  install -Dm644 "${srcdir}/dkms.conf" "${pkgdir}/usr/src/${pkgbase}-${pkgver}/dkms.conf"
  sed -e "s/@PKGBASE@/${pkgbase}/" \
    -e "s/@PKGVER@/${pkgver}/" \
    -i "${pkgdir}/usr/src/${pkgbase}-${pkgver}/dkms.conf"

  install -Dm644 "crypto/cryptodev.h" "${pkgdir}/usr/include/crypto/cryptodev.h"
}
