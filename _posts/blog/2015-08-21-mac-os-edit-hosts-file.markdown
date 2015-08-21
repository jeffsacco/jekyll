---
layout: post
title:  "Edit hosts file on mac os"
date:   2015-08-21 13:39:34
categories: blog
tags: macos
published: true
---

When setting up your own localhost for web development. chances are you will need to edit your hosts file to set up a new virtual host.

The path to the location of the host file is as follows:

	/private/etc/hosts

If this isnt the location, try this command to locate it

	sudo find / -name "hosts"
