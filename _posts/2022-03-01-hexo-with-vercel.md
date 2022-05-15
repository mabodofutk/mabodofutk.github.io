---
layout: post
title: "Hexo with Vercel and Github"
categories: misc
---
Nowadays deploying a hexo powered static blog is quite easy, and with vercel this can be done just in a couple of clicks. However, there're still some problems to solve.  
## Custom domain
On this topic I'll focus on the custom domain which involves both Cloudflare and Vercel.  
Actually, Vercel has already provided an excellent guidance on [*How do I use a Cloudflare domain with Vercel?*](https://vercel.com/support/articles/using-cloudflare-with-vercel)  
Basically, you can configure dns settings on Cloudflare to look like:  

|Type|Name|Content|Proxy status|TTL|
|:---|:---|:---|:---|:---|
|A|@|76.76.21.21|DNS only|Auto|
|CNAME|www|cname.vercel-dns.com|DNS only|Auto|  

Then it will use Vercel cdn directly and `www` prefix urls will lead to apex urls.
## Git submodules
This part is more about blog customizations.  
One of the common topic on deploying Hexo blogs is to configure a custom theme. And with Vercel, there're two conditions to consider.  
* **The theme can be installed with node package**  
  Then it is easy. Just install the package and deploy.
* **The theme exists as github repository without node package**  
  This will lead to using Git submodules.  
  ```bash
  git submodule add <theme_git_url> <path>
  ```
  *Note: Vercel's deploying process does NOT  support `SSH` git urls currently. As a consequence, you'll need to use `https` git urls instead.*  
  After adding git submodules, a `.gitmodules` file will appear in the blog directory.  
  With submodules enabled, when cloning the git repository, instead of using `git clone`, you should use `git clone --recurse-submodules` to include submodules.  

