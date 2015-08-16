# Contributor: Sohaib Afifi <me@sohaibafifi.com>

pkgname=minbar-svn
pkgver=0.3
pkgrel=4
pkgdesc="Islamic prayer times and athan for GNOME"
url="http://djihed.com/minbar"
arch=('i686' 'x86_64')
license=('GPL')
depends=(gtk3 libitl-svn librsvg gstreamer0.10 libnotify gconf hicolor-icon-theme)
makedepends=(gnome-common)
optdepends=('xfce4-xfapplet-plugin: adds Xfce4 panel support')
install=minbar.install
conflicts=('minbar')
source=()
md5sums=()

_svntrunk="https://svn.arabeyes.org/svn/projects/itl/programs/minbar"


build() {
  cd $srcdir/
  msg "Connecting to the $_svnmod SVN server..."
  if [ -d "$_svnmod/.svn" ]; then
    cd minbar && svn up -r $pkgver
    msg2 "Local files updated"
  else
    svn co $_svntrunk --config-dir ./ minbar
    msg2 "SVN checkout done"
  fi
  cd minbar
  msg "Starting make..."
  ./autogen.sh --prefix=/usr --sysconfdir=/etc
  make || return 1
}

package() {
  cd $srcdir/minbar
  make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR=${pkgdir} install
}
