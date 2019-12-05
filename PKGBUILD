pkgname=physfs
pkgver=3.0.2
pkgrel=1
pkgdesc="A library to provide abstract access to various archives"
arch=('x86_64')
url="http://icculus.org/physfs/"
license=('zlib')
depends=('zlib')
makedepends=('cmake' 'doxygen')
source=("http://icculus.org/physfs/downloads/${pkgname}-${pkgver}.tar.bz2")
sha256sums=('304df76206d633df5360e738b138c94e82ccf086e50ba84f456d3f8432f9f863')

build() {
	mkdir build
	cd build
	cmake "../${pkgname}-${pkgver}" -DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_INSTALL_PREFIX=/usr \
		-DPHYSFS_BUILD_TEST=OFF -DPHYSFS_BUILD_WX_TEST=OFF
	make all docs
}

package() {
	cd build
	make DESTDIR="${pkgdir}" install
	install -d "${pkgdir}"/usr/share/{doc/physfs,man/man3}
	install -m644 docs/html/* "${pkgdir}/usr/share/doc/physfs"
	install -m644 docs/man/man3/* "${pkgdir}/usr/share/man/man3"
	for i in author Deinit description extension Free Init major Malloc minor opaque patch Realloc url ; do
		mv "${pkgdir}/usr/share/man/man3/$i.3" "${pkgdir}/usr/share/man/man3/PHYSFS_$i.3"
	done
	install -D -m644 ../${pkgname}-${pkgver}/LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
