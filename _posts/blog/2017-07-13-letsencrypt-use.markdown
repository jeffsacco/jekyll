---
layout: post
title:  "Using Lets Encrypt to generate a third party cert and install it on Bluehost"
date:   2017-07-13 10:27:00
categories: blog
tags: bluehost letsencrypt
published: true
---

So I needed to really get some of my sites onto HTTPS.  I looked into Bluehost where I already have one site on HTTPS but I did that the old fashion way of purchasing it.  I also had to purchase a dedicated IP but that is a sunk cost no matter what.  You need a dedicated IP to run HTTPS.

First thing I did was grab a copy of certbot.  From the terminal I ran:

	brew install certbot

Using homebrew was a welcomed relief.  Took a few minutes but certbot was installed on my machine.

Once installed, I took a look at the variety of methods to generate a certificate.  I know I couldn't install certbot on my bluehost box so I would need to do a manual install.  Luckily certbot does have a manual method to generate one.  A pre-requsite of this is you need to have access to the server to create some directories and files.

The command I used to generate my certificate was:

	certbot certonly --manual -d www.example.com

From this it will ask you a bunch of questions.  At one point it will ask you to create a few directories on your webserver.  It will also ask you to drop a file in this directory with a code.

I was already ssh'ed into my box so I just created a few directories with mkdir, touch filename, vi'ed into that file, dropped the code and continued on with the cert process.

Once the cert is generated, we can check it with this command:

	certbot certificates

This will give a list of the certificate name, expiry date, path and private key.  Now this is where the fun starts.  What we need to do in bluehost is get our private key uploaded to our account.  How do we do this?  First is to log into your admin panel and traverse over to your cpanel.  Looks for the security section and you will see the icon for "SSL/TLS Manager".  Click there and you will be presented with three options.  First is your private key, second is your Certificate Signing Requests and the final one is your certificates.

We start at the private key.  We generated this from our certbot and running certbot certificates tells us the path.  I made is a little easier for me to find the private key by copying it from its secure location to my desktop.  I then uploaded this.

Once uploaded I moved onto step two which is the Certificate Signing Requests.  When on that page, I have the ability to generate one from my private key.  Once this is complete, it will present me with some very cryptic looking text.  This is good because our next step requires this text.  I went over to:

	https://www.comodo.com/

You are able to get a free certificate in three month intervals which is exactly what we need.  I created an account there, placed in my Certificate Signing Request code and was able to generate my certificate.  I downloaded it and then uploaded it on bluehost to the certificate section.

The final step is contacting bluehost to ask them to move your third party certificate onto their server.  They should ask you what domain and confirm it is a third party certificate.  Sometimes they act 'confused' but say you followed their help tutorial here:

	https://my.bluehost.com/cgi/help/204

Thats it.  Refresh your website in https mode and it will pick up.  Usually you will need to edit your .htaccess file if you are running Apache 

	RewriteEngine On 
	RewriteCond %{HTTP_HOST} ^example\.com [NC]
	RewriteCond %{SERVER_PORT} 80 
	RewriteRule ^(.*)$ https://www.example.com/$1 [R,L]

That should give you more than enough explaination to get your free SSL cert.  Enjoy.









