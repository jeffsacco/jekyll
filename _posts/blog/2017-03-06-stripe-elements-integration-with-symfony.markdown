---
layout: post
title:  "Stripes new elements "
date:   2017-03-06 13:39:34
categories: blog
tags: stripe symfony php
published: true
---

Stripe recently depreciated its stripe.js package for handling communication to its payment platform.  I had used it to create various payment capturing forms.  Very easy to implement and use.

Over the weekend, Stripe envailed Stripe elements.  They now produce all the html to render the payment form with a simple div ID.  To faciliate the change you include their javascript:

    <script type="text/javascript" src="https://js.stripe.com/v3/"></script>

and then just include their div:

    <div id="card-element">

    </div>

Of course you will need to include the key which I placed in the parameters.yml file.  No need to inject it directly.  

Now one of the key coding that needs to be done is sending along all the tertiary information about the credit card when it generates the profile on Stripes end.  Taking a look at the function:

    stripe.createToken(card, options)

the stripe.createToken accepts two parameters.  First is the card which is a no brainer.  The second part are the options.  These options are the address, city, state, province, etc which builds a better profile of Stripes Radar to evaluate the riskyness of the card.

Options is just a regular javascript object.  I have placed a sample below:

    var options = {address1: '123 somewhere ave', address2: 'unit 111'}

How do you extract this data?  I used jQuery to grab the values from the form input fields.

Enjoy :+)













