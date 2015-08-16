# $Id: PKGBUILD 187901 2013-06-07 22:39:54Z heftig $
# Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>
# Maintainer: Ionut Biru <ibiru@archlinux.org>
# Contributor: Michael Kanis <mkanis_at_gmx_dot_de>

pkgname=mutter-biggershadows
pkgbasename=mutter
pkgver=3.8.4
pkgrel=1
pkgdesc="A window manager for GNOME, patched for bigger window shadows"
arch=(i686 x86_64)
license=('GPL')
depends=('clutter' 'dconf' 'gobject-introspection' 'gsettings-desktop-schemas' 'libcanberra' 'startup-notification' 'zenity' 'libsm')
makedepends=('intltool' 'gnome-doc-utils')
url="http://www.gnome.org"
groups=('gnome')
options=('!libtool' '!emptydirs')
provides=('mutter')
conflicts=('mutter')
install=mutter.install
source=(http://ftp.gnome.org/pub/gnome/sources/$pkgbasename/${pkgver%.*}/$pkgbasename-$pkgver.tar.xz
	bigger-shadows.patch)
sha256sums=('efe28bb665fd43d97b20c57bb1d1dc0a7e98919b6ad4b770bfd7ec5576e29454'
'0244a4197bf890724c68f9cfb26c4f4303096bdb9e9305f11775d733111e6e64')

build() {
  cp bigger-shadows.patch $pkgbasename-$pkgver/src
  cd "$pkgbasename-$pkgver"
  cd src
  patch -p1 < bigger-shadows.patch
  cd ..
  ./configure --prefix=/usr --sysconfdir=/etc \
      --libexecdir=/usr/lib/mutter \
      --localstatedir=/var --disable-static \
      --disable-schemas-compile --enable-compile-warnings=minimum

  #https://bugzilla.gnome.org/show_bug.cgi?id=655517
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

  make
}

package() {
  cd "$pkgbasename-$pkgver"
  make DESTDIR="$pkgdir" install
}
