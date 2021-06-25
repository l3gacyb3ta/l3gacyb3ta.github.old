
---
title: Domain name, finally
date: 2021-04-14 11:05:28
tags: ["dns", "website"]

---

So, I finally got [l3gacy.tk](l3gacy.tk) linked to the github pages! The process was a bit confusing, probably because I've never done something like this before, but here's the steps I took. 
 
   

First I got a free domain from [freenom.com](freenom). Quick tip, if you want one, write out the full domain in the domain search bar instead of just the first part (i.e. ```example.tk``` instead of just ```example```). Once I had done that, I signed up for a free cloudflare acount, as they have a better domain-name-manegment-system-thing. Then I had to link my domain back to cloudflare, which was supprisingly easy. All I did was set the nameservers in freenom's interface to the ones cloudflare gave me, and I was off to the races! (Well it took a couple hours, so maybe more of a road trip.) 

   

The next step was getting that domain to point to my github pages. So I googled that, and I found a great [https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site](doc page) on how to set a custom domain in github pages (turns out there's just a little textbox in the settings menu that adds a CNAME file). After that, it was a matter of adding some records to my domain in cloudflare, and it works now!  

  

That's all for today folks, stay safe and happy!  

\- l3gacy