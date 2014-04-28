pkgname='python3-scipy'
pkgver=0.13.3
pkgrel=1
pkgdesc="SciPy is a Python-based ecosystem of open-source software for mathematics, science, and engineering."
arch=('x86_64')
url="http://www.scipy.org/"
license=('BSD')
makedepends=('gcc-fortran' 'python3-numpy' 'python3-setuptools')
optdepends=('python3-nose')
source=("https://pypi.python.org/packages/source/s/scipy/scipy-${pkgver}.tar.gz")
md5sums=('0547c1f8e8afad4009cc9b5ef17a2d4d')

build() {
  export LDFLAGS="-Wall -shared"

  cd scipy-${pkgver}
  python3 setup.py config_fc --fcompiler=gnu95 build
}

check() {
  # we need to do a temp install so we can import scipy
  # also, the tests must not be run from the scipy source directory
  export LDFLAGS="-Wall -shared"

  cd ${srcdir}/scipy-${pkgver}
  python3 setup.py config_fc --fcompiler=gnu95 install \
    --prefix=/usr --root=${srcdir}/test --optimize=1
  export PYTHONPATH=${srcdir}/test/usr/lib/python3.3/site-packages
  # cd ${srcdir}
  # python3 -c "from scipy import test; test('full')"
}

package_python3-scipy() {
  depends=('python3-numpy')
  provides=('python3-scipy')

  cd scipy-${pkgver}
  export LDFLAGS="-Wall -shared"

  python3 setup.py config_fc --fcompiler=gnu95 install \
    --prefix=/usr --root=${pkgdir} --optimize=1

  install -Dm644 LICENSE.txt \
    "${pkgdir}/usr/share/licenses/python3-scipy/LICENSE"
}
