#!/bin/bash

# Created from the original PKGBUILD by Caleb Maclennan <caleb@alerque.com>, Guillaume Horel <guillaume.horel@gmail.com> and William Turner <willtur.will@gmail.com>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/python-booleanoperations/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/python-booleanoperations/discussions>

_langname="python"
_relname="booleanOperations"
_pacname="booleanoperations"

pkgname="${_langname}-${_pacname}"
pkgver=0.9.0
pkgrel=4
pkgdesc="A library to provide boolean operations on paths"
arch=(any)
url="https://github.com/typemytype/booleanoperations"
license=(
  "MIT"
)
depends=(
  "python"
  "python-pyclipper"
  "python-fonttools"
)
checkdepends=(
  "python-defcon"
  "python-fontpens"
  "python-pytest"
)
makedepends=(
  "python-setuptools-scm"
)
_zipname="$_relname-$pkgver"
source=(
  "https://files.pythonhosted.org/packages/source/${_relname::1}/${_relname}/${_zipname}.zip"
)
sha512sums=(
  "f06d2d3143399f5f6325456a2368d608ad8b7b18a5f63bdaf4c48ddd9a9a2aebf4f67da5cadad2aa0d9d9caaa4839f314ed016cb8572805ef3a01f74e469e56b"
)

prepare() {

  cd "$_zipname"

  # Upstream PR: https://github.com/typemytype/booleanOperations/pull/63
  sed -i -e '/wheel$/d' setup.cfg
}

build() {

  cd "$_zipname"

  python setup.py build
}

# Upstream (still/again) has circular dependencies in the test suite
# https://github.com/typemytype/booleanOperations/issues/64
# check() {
#     cd "$_zipname"
#     PYTHONPATH=Lib pytest tests
# }

package() {

  cd "$_zipname"

  python setup.py install --root="$pkgdir" --optimize=1 --skip-build

  install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE
}
