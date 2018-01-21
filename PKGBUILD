# Maintainer: sum01 <sum01@protonmail.com>
# Contributor: tommyshem
# Previous Maintainer: Atnanasis <ys2000pro@gmail.com>
# Contributor: Youngbin Han <sukso96100@gmail.com>
pkgname=micro-nightly-bin
pkgver=1.3.5.81
pkgrel=1
pkgdesc="A modern and intuitive terminal-based text editor"
arch=('x86_64' 'i686')
url="https://github.com/zyedidia/micro"
license=('MIT')
depends=('glibc')
makedepends=('grep' 'sed' 'curl' 'wget' 'tar' 'coreutils')
optdepends=('xclip: for copying to and from the terminal')
conflicts=('micro')
provides=('micro')
pkgver() {
	curl -s 'https://api.github.com/repos/zyedidia/micro/releases/tags/nightly' | grep -oEm 1 '[0-9]+\.[0-9]+\.[0-9]+\-(dev\.)?[0-9]+' | sed -E 's/\-(dev\.)?/\./'
}
build() {
	if [[ $CARCH == "i686" ]]; then
		_bits="32"
	else
		_bits="64"
	fi
	if [[ -e "$srcdir/micro" ]]; then
		rm -rf "$srcdir/micro"
	fi
	_realver=$(curl -s 'https://api.github.com/repos/zyedidia/micro/releases/tags/nightly' | grep -oEm 1 '[0-9]+\.[0-9]+\.[0-9]+\-(dev\.)?[0-9]+')
	_filename="micro-$_realver-linux$_bits.tar.gz"
	cd "$srcdir"
	wget "https://github.com/zyedidia/micro/releases/download/nightly/$_filename"
	tar -xvf "$_filename"
	mv -f "$srcdir/micro-$_realver" "$srcdir/micro"
}
package() {
	install -Dsm755 "$srcdir/micro/micro" "$pkgdir/usr/bin/micro"
	install -Dm644 "$srcdir/micro/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
