Persyaratan :
Ubuntu/debian versi 32/64 bit sudah terinstall dengan baik dan bisa ping ke internet, contoh: ping google.com, untuk manual install ubuntu silahkan lihat2 theread disini, sudah banyak, baik yang menggunakan gambar/text

Lets Go try, mari kita oprek :
- Login ke putty dan jadi root (sudo su -)

Silahkan backup / copy dulu confignya lalu remove package lusca/squid yang lama

Code :
cp -Rf /etc/squid /etc/squid-jadul
apt-get purge lusca  lusca-common lusca-cgi

atau

apt-get purge squid squid-common squid-cgi
atau jika pc sudah pernah terinstall  squid/lusca dari sorces

rm -rf /etc/squid
rm -f /usr/sbin/squid

Download package, extract dan install
cd /tmp/

32 bit sedot disini :
wget https://pakmin.googlecode.com/files/deb-htproxy_14942_i386.tar.bz2

64 bit sedot disini :
wget https://pakmin.googlecode.com/files/deb-htproxy_14942_x86-64.tar.bz2

extrack dan install filenya :
32 bit :
tar xvf deb-htproxy\_14942\_i386.tar.bz2 && dpkg -i **.deb**

64 bit
Code:
tar xvf deb-htproxy\_14942\_x86-64.tar.bz2 && dpkg -i **.deb**

cek apakah htproxy dan helper yang baru sudah terinstall, dengan perintah
Code:
squid -v
/usr/lib/squid/hikmah-teknologi.com  -v

jika sudah stop dulu servisnya agar kita bisa membuat cache\_dir yang sesuai
/etc/init.d/squid stop

Edit squid.conf cukup sesuaikan cache\_dir dan cache\_mem,baca comment petunjuknya dulu , silahkan sesuikan partisi cache pada cache\_dir dan DNS pada dns\_nameserver

Code:
nano /etc/squid/squid.conf

lalu simpan dengan menekan control x dan enter jika sudah ubah kepmilikan cache\_dir dengan user:group proxy: proxy (tanpa spasi setelah titik dua) lalu buat cache swap dengan perintah

Code:
chown proxy:proxy /cache**squid –z**

jika sudah oke, jalankan servicesnya

Code:
/etc/init.d/squid start

silahkan cek apakah servis sudah jalan dengan perintah

Code:
netstat -pln |grep squid

jika sudah ada penampakan :
tcp        0      0 0.0.0.0:3128  0.0.0.0:**LISTEN**

**Untuk mengaktifkan blocking porno pada situs pencarian, ada perbaikan pada confignya.sebelumnya**

Code:
#inlude /etc/squid/safeSearch.conf

ganti jadi seperti ini :

Code:
include /etc/squid/safeSearch.conf