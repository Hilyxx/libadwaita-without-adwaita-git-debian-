# Maintainer: ich <remove dashes in s-c--25-ni at gmail dot com>

pkgname=libadwaita-without-adwaita-git
pkgver=1.4.0
pkgrel=5
url="https://gnome.pages.gitlab.gnome.org/libadwaita"
pkgdesc='libadwaita; Includes a patch to not overwrite the system theme'
arch=('i686' 'x86_64' 'armv7h' 'armv6h' 'aarch64')
license=('LGPL')

provides=("libadwaita=${pkgver}" "libadwaita-1.so=0-64")
conflicts=('libadwaita')

source=(
    "${pkgname}::git+https://gitlab.gnome.org/GNOME/libadwaita"
    theming_patch.diff
)
sha256sums=(
    SKIP
    SKIP
)

depends=('libgtk-4-1')
makedepends=(git meson gi-docgen sassc gobject-introspection valac pkg-config patch cmake meson libsass1 gcc)

build() {
  cd "${srcdir}/${pkgname}"
  git checkout "${pkgver}"
  <"${srcdir}"/theming_patch.diff patch src/adw-style-manager.c
  meson build --prefix=/usr -Dexamples=false
  ninja -C build 
}

package() {
  cd "${srcdir}/${pkgname}"
  DESTDIR="$pkgdir" ninja -C build install
}
