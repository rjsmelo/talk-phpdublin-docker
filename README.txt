== Simple Docker ==

docker run centos:6 cat /etc/redhat-release
docker run -ti centos:6 bash

== Docker Hub ==

docker pull ubuntu
docker run -ti ubuntu bash
apt-get update
apt-get install figlet
figlet phpDublin.com
docker commit -m 'figlet app' -a 'Ricardo Melo' 7c367550ba16 rjsmelo/figlet-phpdublin
docker push rjsmelo/figlet-phpdublin

== Fig up ==

docker-compose build
docker-compose up
docker-compose up -d
browser (fireproxy) -> x.p55 -> x.p56 -> x.p70

== Wordpress ==
untgz wordpress

docker-compose run php55 bash
mysql -h mysql -u root -p
create database wordpress;

- install using interface
cd /Users/rmelo/work/docker/php-dublin/sites/wordpress/wp-content/themes/twentysixteen/
vim header.php (search get_header_image)

<h1 style="background-color:red;"><?php echo phpversion(); ?></h1>



== Cleanup ==
docker-compose kill
docker-compose rm


