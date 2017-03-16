---
layout: post
title:  "Drupal 7 and Search API with solr.  Exception handling override"
date:   2017-03-16 10:27:00
categories: blog
tags: drupal solr 
published: true
---

So I get a request from business that they want to override the default solr error message when solr isn't reachable.

I showed them the default error message but they were not happy with this.  So my search began to figure this one out.

I first started with a usual google search on overriding drupal error messages.  Nothing good came up.  So I hunted down where this actual message was being spit out.  Turned out it was using the Exception class.  Perfect!  I can just extend this and override it

    class SearchApiException extends Exception {

    public function __construct($message = NULL) 
    {
        if (!$message) 
        {
        $message = t('An error occurred in the Search API framework.');
        }
    
        if('"0" Status: Request failed: No connection could be made because the target machine actively refused it.')
        {   
            parent::__construct('This is where my custom message would be.');
        }
        else
        {
            parent::__construct($message);
        }
    
    }

}














