# Maintainer: Mattias Andrée <`base64 -d`(bWFhbmRyZWUK)@member.fsf.org>
pkgname=xz-java-git
pkgver=20130129
pkgrel=1
pkgdesc="Java library for XZ and LZMA compression"
arch=('any')
url="http://tukaani.org/xz/java.html"
license=('Public Domain')
depends=('java-runtime>=1.4')
makedepends=('git' 'java-environment>=1.4')
provides=('xz-java')
conflicts=('xz-java')

_gitroot=http://git.tukaani.org/xz-java.git
_gitname=xz-java

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  javac -source 1.4 -target 1.4 -d . -s src -cp . $(find src | grep \\.java\$)
  jar -cf xz-java.jar $(find . | grep \\.class\$)
}

package() {
  cd "$srcdir/$_gitname-build"
  install -d "$pkgdir/usr/lib/"
  install -m 755 xz-java.jar "$pkgdir/usr/lib/"
}
