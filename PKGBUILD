# Maintainer: Taiki Sugawara <buzz.taiki@gmail.com>

pkgname=oracle-xe-11g
_ver=11.2.0
_rel=1.0
pkgver=${_ver}_${_rel}
pkgrel=1
pkgdesc="a non free DBMS"
url="http://www.oracle.com/"
license=('custom')
arch=('x86_64')
conflicts=('oracle-xe')
provides=('oracle-xe')
options=('!strip')
depends=('libaio>=0.3.104' 'gcc>=4.1.2' 'binutils>=2.16.91.0.5' 'make>=3.80' 'glibc>=2.3.4-2.41' 'zip' 'unzip')
makedepends=('rpmextract')
install='oracle.install'
source=("oracle-xe-${_ver}-${_rel}.x86_64.rpm.zip" "LICENSE" "oracle-xe")
md5sums=('dd7881a55569d890241f11cd0eeb7d48' '0e8646f7081283d24671b938dabd0fbe' '778f2e10f606b5d0ee8532c31c0611f8')
# Default value of memory_target parameter
_memory_target=256M

package() {
  local oracle_home=u01/app/oracle/product/11.2.0/xe

  (cd $pkgdir && rpmextract.sh $srcdir/Disk1/oracle-xe-${_ver}-${_rel}.x86_64.rpm)

  install -Dm755 $srcdir/oracle-xe $pkgdir/etc/rc.d/oracle-xe
  rm -rf $pkgdir/etc/init.d

  install -d $pkgdir/etc/profile.d
  ln -s ../../$oracle_home/bin/oracle_env.sh $pkgdir/etc/profile.d/oracle_env.sh
  rm $pkgdir/$oracle_home/bin/{zip,unzip}

  sed -i "s/%memory_target%/$_memory_target/g" $pkgdir/$oracle_home/config/scripts/init.ora 
  chmod 755 $pkgdir/$oracle_home/config/scripts/*.sh

  install -Dm644 LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}
