+++
title = "Dont Yell at Me With Your Twenty Five Dollar Site"
description = ""
author = "Doug"
date = 2022-06-04T05:09:10Z
tags = []
draft = false
+++

I've seen mention on [Hacker News](https://news.ycombinator.com/) of the quote "Don't yell at me with your $X website!"  Whereby X is an arbitrary number meant that just because your site is dynamic and has a spiffy domain doesn't mean you've made a great monetary investment in the cause/site.

This got me thinking, what could I do, that could scale, but still be as dirt cheap as possible.  So of course I am going to cheat, there is nothing but static HTML on this site.  So therefore it should be relatively easy to scale, which lead me to wonder why not just use a CDN to host the site?  Then I needed something formal and static, so I figured I'd go with the tried and true S3 from AWS.  To curate all of this static data I decided to use a static site generator called [hugo](https://gohugo.io/getting-started/quick-start/).

To get the site ready to host static pages, I needed the S3 bucket to host it from and way for that bucket to load [amiblocked.io](https://www.amiblocked.io) (this site) up. I decided to use terraform to make all of this infrastructure implementation possible.  So I ventured out to find the solution to do what appeared to be this relatively simple task.

First, I started [with this guide](https://www.alexhyett.com/terraform-s3-static-website-hosting) and that got me a mostly working code.  The main thing I changed was to make the code happy with terraform and compatible with hugo static sites.  Which led to my first gotcha, hugo generates pages with directories.  For instance the first post on this site is hosted technically at *https://www.amiblocked.io/post/I-did-this-all-on-my-ipad/index.html* , but hugo doesn't actually include the index.html.  I found a module that rewrites requests to */* be instead sent to */index.html*.  Which allowed cloudfront to remain the origin of the request and I didn't have to expose my S3 bucket directly to the internet.

Just to over engineer the entire process I created a github set of workflow actions to first test and create the terraform plan upon the creation of a PR into main and then an action to apply the terraform plan on a commit to main.  This took my need for the usage of terraform cloud or a separate server/workstation to compile and apply the terraform code away completely.  I was interested in not using a service outside of github and AWS for this venture so that helped keep costs down and also gave me a viable workflow alternative to using terraform cloud.

All of the terraform code can be found in this repo [https://github.com/superdug/terraform-amiblocked](https://github.com/superdug/terraform-amiblocked)

I wanted the site to be dynamic, so I opted to use Hugo to make the static site itself.  I cheated a little bit and used a workstation to initially develop the site before getting it ready to be managed by github entirely.  One caveat is that the site is setup to use [Foresty](https://app.forestry.io/login) if I so desire to have a web based management of my site for future collaborations not needing to use git alone.  However, that was out of the scope of this project,  so all posts and code for the site are developed at github.com either using the file editor or using the full IDE environment by switching the .com to .dev on any github page to get a full VS Code shell right there in your browser.

Keeping with over engineering the site there is an action to compile the hugo page into static HTML and then upload it to S3 while invalidating the cache at the cloudfront CDN so that changes appear immediately.

All of the hugo code and actions can be found in this repo [https://github.com/superdug/amiblocked-website](https://github.com/superdug/amiblocked-website)

It costs $0.50 to host the DNS zome of amiblocked.io and pennies to serve the static HTML from the S3 bucket through cloudfront. The domain was $15, so I can yell at you for less than $25 a year in hosting costs with an entirely over engineered dynamic website.

I hope to knock the costs down further in my next iteration that will use cloudflare R2 and pages to host the site.  It's already covered [here](https://developers.cloudflare.com/pages/framework-guides/deploy-a-hugo-site/) how to do it if you want to beat me to the punch and setup a site that costs less than $20 a year to deploy after you pay for registration of the domain and a years worth of hosting.  Bonus, if the site blows up and you get a ton of traffic, you're already setup to handle it.

I'm holding off on that project because what I really want to do is implement cloudflares new [D1 Cloud SQL Database](https://blog.cloudflare.com/introducing-d1/) and their edge workers to make a truly dynamic site that uses a serverless database store as well.
