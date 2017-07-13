---
layout: post
title:  "Mailchimps interest id's are not that easy to locate"
date:   2017-03-07 10:27:00
categories: blog
tags: mailchimp api
published: true
---

Mailchimp makes a lot of things quite easy to implement but this one was a little tricky.  I had created a group with some items inside the group.  I really wanted the user when signing up to a mailing list to segment themselves instead of just getting blasted with any ole email.

In doing this, the API, which calls groups "interests", asks for the key of the json object to be the id of the interest.  No problem.  But where do you find this id?  I did the usual web developer trick of heading over to where the group and group items were created, hovered over the links and see if I could see the id in the url.  This didn't work.

I did a quick search and it looks like the id's can only been seen if you access the API and ask the group and group items.

From there you can see the group item ID's.  When plugging them in, all worked fine.

Hope this helps someone out. 














