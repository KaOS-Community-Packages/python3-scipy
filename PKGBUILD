pkgname='python3-scipy'
pkgver=0.15.0
pkgrel=1
pkgdesc="SciPy is a Python-based ecosystem of open-source software for mathematics, science, and engineering."
arch=('x86_64')
url="http://www.scipy.org/"
license=('BSD')
makedepends=('gcc-fortran' 'python3-numpy' 'python3-setuptools')
optdepends=('python3-nose')
source=("https://pypi.python.org/packages/source/s/scipy/scipy-${pkgver}.tar.gz")
md5sums=('639112f077f0aeb6d80718dc5019dc7a')

build() {
  export LDFLAGS="-Wall -shared"

  cd scipy-${pkgver}
  python3 setup.py config_fc --fcompiler=gnu95 build
}

package() {
  depends=('python3-numpy')
  provides=('python3-scipy')

  cd scipy-${pkgver}
  export LDFLAGS="-Wall -shared"

  python3 setup.py config_fc --fcompiler=gnu95 install \
    --prefix=/usr --root=${pkgdir} --optimize=1

  install -Dm644 LICENSE.txt \
    "${pkgdir}/usr/share/licenses/python3-scipy/LICENSE"
}
