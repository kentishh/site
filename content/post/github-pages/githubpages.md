---
title: "Switching to Github Pages"
description: 
date: 2024-01-06T18:14:36Z
image: 
math: 
license: 
hidden: false
comments: false
draft: false
---
It took me a few years to realise that running a VPS to host a simple blog and VPN (which I never use!) probably wasn't worth the £5 I was spending a every month keeping it up and running. After chatting to a friend, I realised that a better option would be hosting a blog using Github pages. After a few hours I'd copied the posts from my old site, decommissioned my VPS and started getting to work using this amazing [Github repo](https://github.com/CaiJimmy/hugo-theme-stack-starter). The site is still composed using Hugo and this repo contains the requires Hugo modules to test everything within a Github codespace. Amazing!

I was really surprised at just how easy the process was, after a few [DNS changes](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site) everything was back up and running in the space of 3-4 hours. This also introduced me to Github codespaces which is a dream to use, instead of having to compose articles locally, SFTP them over to my VPS and run Hugo manually, the process is now as simple as spinning up the codespace, writing my article in VSCode, commiting my changes and pushing. A Github action takes over to ensure there are no Hugo errors and emails me with any failures/alerts. I may record a tutorial on getting this setup to share here.