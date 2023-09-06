# Maintainer: 7k5x <7k5xlp0onfire@gmail.com>
# Contributor: Whemoon Jang <palindrom615@gmail.com>
# Contributor: Hodong Kim <nimfsoft@gmail.com>
# Contributor: Youngbin Han <sukso96100@gmail.com>
# Contributor: Changjoo Lee <icj7061@gmail.com>
# Contributor: ywen407 <ywen407@naver.com>

# Nimf with libhangul-3beol. Based on nimf-1.3.1.3da51ab
# https://github.com/hamonikr/nimf
# https://gitlab.com/3beol/nimf
pkgname=nimf-3beol
pkgver=r1055.e57f046
pkgrel=1
pkgdesc="Nimf is a lightweight, fast and extensible input method framework."
arch=('any')
url="https://github.com/delvier/nimf"
license=('LGPL3')
depends=(
         'glibc'
         'gtk3'
         'glib2'
         'libhangul-3beol'
         'libappindicator-gtk3'
         'libxkbcommon>=0.5.0'
         'libxklavier'
         'qt5-base'
         'wayland')
makedepends=(
    'git'
        'gcc'
        'intltool'
        'gtk-doc'
        'gtk2'
        'gtk-update-icon-cache'
        'librsvg'
        'libx11'
        'wayland-protocols'
)
conflicts=("nimf" "nimf-git")
provides=("nimf")
source=( "nimf::git+${url}.git" )
md5sums=('SKIP' )

pkgver() {
        cd "$srcdir/nimf"
        printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

post_install() {
        echo "Compiling schemas..."
        /usr/bin/glib-compile-schemas /usr/share/glib-2.0/schemas/
        echo "Running ldconfig..."
        ldconfig
        echo "Updating GTK icon cache..."
        gtk-update-icon-cache
        echo "Updating immodules cache..."
        gtk-query-immodules-3.0 --update-cache
        gtk-query-immodules-2.0 --update-cache
}

post_upgrade() {
        post_install $1
}
build() {
        cd "$srcdir/nimf"
        ./autogen.sh --prefix=/usr
        make
}

package() {
    rm -rf $srcdir/../nimf
        cd "$srcdir/nimf"
        make DESTDIR="${pkgdir}/" install
}
