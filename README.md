# Install-ImageMagick-EasyApache4
Quick Guide to install ImageMagick in Easy Apache 4
--
Take from: https://help.bigscoots.com/en/articles/730428-cpanel-easyapache-4-installing-imagemagick-and-imagick-php-extension

1. Installing imagemagick:

`yum -y install ImageMagick-devel ImageMagick-c++-devel ImageMagick-perl`

2. Installing the imagemagick PHP extensions for all installed PHP versions.
```
for phpver in $(whmapi1 php_get_installed_versions|grep -oE '\bea-php.*') ; do
printf "\autodetect" | /opt/cpanel/$phpver/root/usr/bin/pecl install imagick
echo 'extension=imagick.so' >> /opt/cpanel/$phpver/root/etc/php.d/imagick.ini
done
/scripts/restartsrv_httpd
/scripts/restartsrv_apache_php_fpm
```

3.  Test to make sure imagemagick is installed:

`/usr/bin/convert --version`

4. Test to make sure the PHP extensions loaded:
```
for phpver in $(whmapi1 php_get_installed_versions|grep -oE '\bea-php.*') ; do
echo "PHP $phpver" ; /opt/cpanel/$phpver/root/usr/bin/php -m |grep imagick
done
```
