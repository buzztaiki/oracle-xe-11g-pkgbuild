# Maintainer: Taiki Sugawara <buzz.taiki@gmail.com>

pkgname=oracle-xe-11g
_ver=11.2.0
_rel=1.0
_rpm=oracle-xe-${_ver}-${_rel}.x86_64.rpm
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
source=("$_rpm" "LICENSE" "oracle-xe")
md5sums=('3371612d47e1a0a4cc8f53470b1f4fe3' '0e8646f7081283d24671b938dabd0fbe' 'a9d9be34defc0b599c713d13dd605187')
# Default value of memory_target parameter
_memory_target=256M

package() {
  local oracle_home=u01/app/oracle/product/11.2.0/xe

  cp -a {etc,usr,u01} $pkgdir

  install -Dm755 $srcdir/oracle-xe $pkgdir/etc/rc.d/oracle-xe
  rm -rf $pkgdir/etc/init.d

  install -d $pkgdir/etc/profile.d
  ln -s ../../$oracle_home/bin/oracle_env.sh $pkgdir/etc/profile.d/oracle_env.sh
  rm $oracle_home/bin/{zip,unzip}

  sed -i "s/%memory_target%/$_memory_target/g" $pkgdir/$oracle_home/config/scripts/init.ora 
  chmod 755 $pkgdir/$oracle_home/config/scripts/*.sh

  install -Dm644 LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}
