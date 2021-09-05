# Maintainer: Sick Codes <info a t sick dot codes>
# Contributor: Tobias Martin <tm-x at gmx dot net>

_pkgbase=anbox-modules
pkgname=anbox-modules-dkms
pkgver=5
_extramodules="$(uname -r)"
pkgrel=7
pkgdesc="Android kernel driver (binder, ashmem) in DKMS format"
arch=('i686' 'x86_64')
license=('GPLv3')
provides=($pkgname)
depends=('linux-headers')
# source=("https://github.com/choff/anbox-modules/archive/refs/heads/master.zip")
source=("git+https://github.com/sickcodes/anbox-modules.git")
sha256sums=('SKIP')

# prepare() {
#   unzip "master.zip"
# }

build() {

  cd "${srcdir}/anbox-modules/binder"
  msg2 "Building binder..."
  make

  cd "${srcdir}/anbox-modules/ashmem"
  msg2 "Building ashmem..."
  make
}

_get_package_version() {
  grep PACKAGE_VERSION "${srcdir}/anbox-modules/${1}/dkms.conf" | sed -r 's#PACKAGE_VERSION="([0-9.]+)"#\1#'
}

package() {
  _dkms_version_binder="$(_get_package_version binder)"
  _dkms_version_ashmem="$(_get_package_version ashmem)"

  dkms_dir_binder="${pkgdir}/usr/src/anbox-ashmem-$_dkms_version_ashmem/"
  dkms_dir_ashmem="${pkgdir}/usr/src/anbox-binder-$_dkms_version_binder/"

  mkdir -p "${pkgdir}/usr/lib/modules/${_extramodules}"

  cd "${srcdir}/anbox-modules/binder"
  mkdir -p "$pkgdir/usr/src/${dkms_dir_binder}"
  install -Ddm755 "${dkms_dir}"
  install -D -m644 "${srcdir}/anbox-modules/binder/dkms.conf" "$pkgdir/usr/src/${dkms_dir_binder}/dkms.conf"
  make DESTDIR="${pkgdir}/usr/lib/modules/${_extramodules}" install

  cd "${srcdir}/anbox-modules/ashmem"
  mkdir -p "$pkgdir/usr/src/${dkms_dir_ashmem}"
  install -D -m644 "${srcdir}/anbox-modules/ashmem/dkms.conf" "$pkgdir/usr/src/${dkms_dir_ashmem}/dkms.conf"
  make DESTDIR="${pkgdir}/usr/lib/modules/${_extramodules}" install

}

# vim:set ts=2 sw=2 et:
