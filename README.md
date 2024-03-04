# ApacheDS
ApacheDS is a free and opensource simple directory management software. If you need to quickly setup LDAP for any of your projects , ApacheDS will be the easiest and most prominent solution. There are some advance and feature-full solutions such as FreeIPA but setup will be a pain in the ass for developers (if you are not from DevOps background)

Unfortunately there are no official images in the Docker Hub for ApacheDS. Here are some simple steps to up and run your own docker based LDAP server !

FROM openjdk:11.0.5-slim-buster

RUN apt-get update

RUN apt-get install wget procps -y

WORKDIR /tmp

RUN wget https://www-us.apache.org/dist//directory/apacheds/dist/2.0.0.AM25/apacheds-2.0.0.AM25-amd64.deb

RUN chmod +x apacheds-2.0.0.AM25-amd64.deb

RUN dpkg -i apacheds-2.0.0.AM25-amd64.deb

RUN apt-get -f install

RUN mv /etc/init.d/apacheds-2.0.0.AM25-default /etc/init.d/apacheds

RUN service apacheds restart

EXPOSE 10389 10636
view rawApacheDS_Dockerfile hosted with ❤ by GitHub
Build the ApacheDS Image
docker build -t apacheds 
Run the container
docker run -dt --name apacheds_container -p 389:10389 -p 636:10636 apacheds:latest
Here we expose 336 as our LDAP port to outside world


LDAP Clients
There are various LDAP clients available to examine and view directory structures.

http://directory.apache.org/studio/
http://jxplorer.org/
It is recommended to use Apache Directory Studio but for a quick demo I will use JXplorer (default admin password is ‘secret’)
