
---
title: Got this working on github pages!
date: 2021-04-13 15:28:00
tags: ["dns", "ghpages", "github"]
---



Well, this was a pain in the butt.  

I didn't feel like messing with github actions again, as I _hate_ that thing with a **passion**. So I was looking through the hexo docs and I found a usefull one-command deploy option. All you have to do is add this little tidbit to your _config.yaml.  

```

deploy:

  type: git

  repo: https://github.com/<username>/<project>

  # example, https://github.com/l3gacyb3ta/l3gacyb3ta.github.io

  branch: <whatever branch you use>

```  

You also have to install hexo-deployer-git, which is simple, just use this:  

```$ npm install hexo-deployer-git --save```  

  

And then all you have to do to deploy is:  

```$ hexo deploy```

  

That was easy!  