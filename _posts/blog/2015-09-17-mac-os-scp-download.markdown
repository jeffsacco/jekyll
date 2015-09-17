---
layout: post
title:  "Downloading a file from a remote host via scp"
date:   2015-09-17 13:39:34
categories: blog
tags: mac
published: true
---

Here is a command I something use when either compressing some files on a server via ssh.  Sometimes I won't have access via FTP to download a file but I do have this alternative to download it.

The first part of the command looks very similar to the ssh command.  Just replace what you need to.  If the file is right where you login, then you don't need to put a path in.  Otherwise you will need to.

The second part is where you want to save the file locally.

	scp your_username@remotehost.edu:foobar.txt /local/dir