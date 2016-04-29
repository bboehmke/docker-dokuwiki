DokuWiki Docker Container
=========================

(based on the original image from M. Prasil: https://bitbucket.org/mprasil/docker_dokuwiki)

Start:
------

	docker run -d -p 8080:80 --name wiki_instance dtwardow/dokuwiki 

Visit the install page (http://<host-ip>:8080/install.php) to configure your
new DokuWiki instance, now.

Upate Image:
------------

First stop your container

	docker stop wiki_instance

Then run new container just to hold the volumes

	docker run --volumes-from wiki_instance --name wiki_data /bin/true

Now you can remove old container

	docker rm wiki_instance

..and run a new one (you built, pulled before)

	docker run -d -p 80:80 --name wiki_instance --volumes-from wiki_data dtwardow/dokuwiki 

afterwards you can remove data container if you want or keep it for next update

	docker rm wiki_data

Optimizing:
-----------

Lighttpd configuration also includes rewrites, so you can enable 
nice URLs in settings (Advanced -> Nice URLs, set to ".htaccess")

For better performance enable xsendfile in settings.
Set to proprietary lighttpd header (for lighttpd < 1.5)

Build your own
--------------

	docker build -t own_dokuwiki .
