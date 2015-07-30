---
layout: post
title:  "Drupal 6 content type theme preprocess"
date:   2015-07-28 09:13:34
categories: blog
tags: php drupal
---

For anyone who is still working on a Drupal 6 site, this little piece of code will help you on the themeing side.

If you want to directly target a content type so you can spin off a page template, this will do it for you.


	function theme_preprocess_page(&$variables) 
	{ 
		if (!empty($variables['node']) && !empty($variables['node']->type)) 
		{ 
			$variables['template_files'][] = "page-node-" . $variables['node']->type;
		}
	}


Change out `theme` on the function name to your own theme name.  Clear the cache and run cron to see the effect.

