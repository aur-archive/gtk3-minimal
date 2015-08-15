# Maintainer: simargl < archpup@gmail.com >

pkgname=gtk3-minimal
pkgver=3.8.2
pkgrel=3
pkgdesc="Multi-platform toolkit for creating graphical user interfaces."
arch=(i686 x86_64)
url="http://www.gtk.org/"
depends=(atk cairo gtk-update-icon-cache libxcursor libxinerama libxrandr libxi
         libxcomposite libxdamage pango shared-mime-info at-spi2-atk)
makedepends=()
options=('!libtool' '!docs')
license=(GPL)
source=(http://ftp.gnome.org/pub/gnome/sources/gtk+/${pkgver%.*}/gtk+-$pkgver.tar.xz)
sha512sums=('20958c192fe881281f6885e2d7cecc4e2700fc01ef8006304f1fb8befe8f6628cbdb06c0d801f109e5805d58f327ca9a07d5e2c7f938116c99db8080d0c2f83e')
conflicts=('gtk3')
provides=('gtk3')
replaces=('gtk3')

build() {
	cd "gtk+-$pkgver"

#export CFLAGS and CXXFLAGS

	CPPFLAGS="-pipe -Wall -Os -march=native"
	CFLAGS=$CPPFLAGS
	CXXFLAGS=$CPPFLAGS
	
	./configure 			\
	--disable-schemas-compile	\
	--enable-introspection=no	\
	--disable-colord		\
	--disable-modules		\
	--disable-Bsymbolic		\
	--disable-xinerama		\
	--disable-gtk-doc		\
	--disable-cups			\
	--disable-papi			\
	--disable-packagekit		\
	--enable-x11-backend		\
	--disable-win32-backend		\
	--disable-quartz-backend	\
	--disable-wayland-backend	\
	--enable-gtk2-dependency	\
	--disable-man			\
	--disable-debug			\
	--disable-static

#	sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

	make -j

#remove uneeded files:

#	rm -rf demos
#	rm -rf docs

#compress files:	



}

package() {
  cd "gtk+-$pkgver"
  make DESTDIR="$pkgdir" install

	cd $pkgdir

#remove unneeeded files and directories

#       rm -rf etc
#	rm -rf usr/share/gtk-3.0
#	rm -rf usr/share/locale
#	rm -rf usr/share/man
#       rm -rf usr/local/include
#       rm -rf usr/local/etc
#       rm -rf usr/local/lib/gtk-3.0
#       rm -rf usr/local/share/themes/Emacs

#	rm -f  usr/local/bin/gtk3-demo
#	rm -f  usr/local/bin/gtk3-demo-application
#       rm -f  usr/local/bin/gtk3-widget-factory
#	rm -f  usr/local/lib/pkgconfig/gtk+-unix-print-3.0.pc
#	rm -f  usr/local/share/glib-2.0/schemas/org.gtk.Demo.gschema.xml
	

#strip symbols, compress libraries:
	strip --strip-unneeded usr/local/lib/libgailutil-3.so.0.0.0
	strip --strip-unneeded usr/local/lib/libgdk-3.so.0.800.2
	strip --strip-unneeded usr/local/lib/libgtk-3.so.0.800.2

}

#note for post installation removal of files:
#usr/local/share/aclocal
