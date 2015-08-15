# Maintainer: spider-mario <spidermario@free.fr>
pkgname=chipmunkpp-git
pkgver=2014.01.13
pkgrel=1
epoch=1
pkgdesc="C++11 wrapper for Chipmunk"
arch=(i686 x86_64)
url="http://bixense.com/chipmunkpp/"
license=('unknown')
depends=(chipmunk)
makedepends=(git scons)
optdepends=('doxygen: to build the documentation')
provides=(chipmunkpp)
conflicts=(chipmunkpp)
source=(git+https://github.com/jhasse/chipmunkpp.git include-path.patch)
sha512sums=(SKIP e413ddcd27ec0ca28f7e3553fd0e4ef5c1a1560052e109d6e61950ddcbedabc37c5ab722b69e632add28e95ff1b91cb2b4132559ee5ffc77a397dc81db148185)

pkgver() {
	cd chipmunkpp
	git log -1 --format='%cd' --date=short | tr - .
}

prepare() {
	cd chipmunkpp
	git apply --3way "$srcdir/include-path.patch"
}

build() {
	cd chipmunkpp

	scons

	if which doxygen > /dev/null 2>&1; then
		cd doc
		doxygen
	fi
}

package() {
	cd chipmunkpp

	install --directory "$pkgdir/usr/"{include,lib}
	pushd src
		find -iname '*.hpp' -exec cp --parents '{}' "$pkgdir/usr/include/" ';'
	popd
	cp *.a "$pkgdir/usr/lib/"

	if [ -d doc/html ]; then
		install --directory "$pkgdir/usr/share/doc/chipmunkpp"
		cp --recursive doc/html "$pkgdir/usr/share/doc/chipmunkpp/"
	fi
}
