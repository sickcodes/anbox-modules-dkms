# Maintainer: Sick Codes <info a t sick dot codes>
# Contributor: Tobias Martin <tm-x at gmx dot net>

pkgname=anbox-modules-dkms
pkgver=4
_extramodules=extramodules-4.10-ARCH
pkgrel=2
pkgdesc="Android kernel driver (binder, ashmem) in DKMS format"
arch=('i686' 'x86_64')
license=('GPLv3')
provides=($pkgname)
depends=('linux-headers')
source=("https://github.com/choff/anbox-modules/archive/refs/heads/master.zip")
sha256sums=('SKIP')

prepare() {
  unzip "master.zip"
}

build() {

  cd "${srcdir}/kernel/binder"
  msg2 "Building binder..."
  make

  cd "${srcdir}/kernel/ashmem"
  msg2 "Building ashmem..."
  make
}

package() {
  mkdir -p "${pkgdir}/usr/lib/modules/${_extramodules}"
  cd "${srcdir}/kernel/binder"
  mkdir -p "$pkgdir/usr/src/binder"
  install -D -m644 "$srcdir/kernel/binder/dkms.conf" "$pkgdir/usr/src/binder/dkms.conf"
  make DESTDIR="${pkgdir}/usr/lib/modules/${_extramodules}" install

  cd "${srcdir}/kernel/ashmem"
  mkdir -p "$pkgdir/usr/src/ashmem"
  install -D -m644 "$srcdir/kernel/ashmem/dkms.conf" "$pkgdir/usr/src/ashmem/dkms.conf"
  make DESTDIR="${pkgdir}/usr/lib/modules/${_extramodules}" install
}

# vim:set ts=2 sw=2 et:
