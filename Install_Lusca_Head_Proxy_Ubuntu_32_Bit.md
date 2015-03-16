Pastikan paket-paket berikut telah terinstall di ubuntu 32 anda

apt-get install squid squidclient squid-cgi gcc build-essential sharutils ccze libzip-dev automake1.9

Dan download source lusca\_fmi ke ubuntu 32 milik anda
cd /usr/src

wget http://pakmin.googlecode.com/files/LUSCA_HEAD-r14809.tar.gz

Extract Lusca head proxy nya :
tar -zxvf LUSCA\_HEAD-[r14809](https://code.google.com/p/pakmin/source/detail?r=14809).tar.gz

Compile Lusca, masuk ke directory LUSCA\_HEAD-[r14809](https://code.google.com/p/pakmin/source/detail?r=14809) dengan perintah :
cd /usr/src/LUSCA\_HEAD-[r14809](https://code.google.com/p/pakmin/source/detail?r=14809)

./configure --prefix=/usr \
--exec\_prefix=/usr --bindir=/usr/sbin\
--sbindir=/usr/sbin --libexecdir=/usr/lib/squid \
--sysconfdir=/etc/squid \
--localstatedir=/var/spool/squid\
--datadir=/usr/share/squid\
--enable-async-io=24 --with-aufs-threads=24 \
--with-pthreads --enable-storeio=aufs \
--enable-linux-netfilter --enable-arp-acl --enable-epoll \
--enable-removal-policies=heap --with-aio --with-dl \
--enable-snmp --enable-delay-pools --enable-htcp \
--enable-cache-digests --disable-unlinkd \
--enable-large-cache-files --with-large-files \
--enable-err-languages=English \
--enable-default-err-language=English \
--with-maxfd=65536

Kemudian build Lusca Head Proxynya :
Make && make install

Matikan squid yang berjalan :
squid -k shutdown
atau
squid stop
atau
service squid stop
atau
/etc/init.d/squid stop

Ubah configurasinya dengan configurasi yang sudah di optimasi, dan sesuaikan dengan jaringan anda :
cd /etc/squid
wget http://nst.web.id/squid.conf

Kemudian ambil juga file storeurl.pl letakkan di /etc/squid

wget http://nst.web.id/storeurl.txt

ubah namanya storeurl.txt menjadi storeurl.pl

dengan caranya :
mv /etc/squid/storeurl.txt /etc/squid/storeurl.pl

Ubah permisionnya :
chown proxy:proxy /etc/squid/storeurl.pl
chmod 777 /etc/squid/storeurl.pl
chmod 600 /etc/squid/squid.conf

Ubah permition directory cache :
chmod 777 /cache
chown proxy:proxy /cache

Buat Swap untuk cache\_dir :
squid -z
atau dengan perintah :
squid -f /etc/squid/squid.conf -z

Jalankan squidnya :
squid -N -d 1 -D