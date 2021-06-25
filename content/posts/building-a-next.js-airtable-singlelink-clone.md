---
title: Building a Next.js + Airtable singlelink clone.
date: 2021-05-15
---
# Singlelink cloned

## Backstory

Recently, something fun happened! I got my first real commission of a website, and it just so happened that I had basically written it earlier that day. I had been building a site for a hackathon I might run at some point, and I wanted to be able to have it not be hard-coded and be more user-friendly than mdx.

I had recently learned about [Airtable](https://airtable.com) thanks to [Hackclub](https://hackclub.com), so I thought why not use this? And in about an hour I had a working demo. I then thought I was done and I was going to move on from that project, but the universe had other plans! Specifically, my good friend asked me to make a website for them. I was a bit worried at first that it would be something I can't do, but they just wanted a singlelink-like thing for their TikTok (If I get permission from them, I'll link it here). 

So I just took the code I had written earlier and adapted it into [Multilink](https://github.com/l3gacyb3ta/multilink)! Obviously, it's FOSS, so it's on GitHub!

## Analytics

For the analytics system, I chose [umami](https://umami.ls). Umami is open-source, and it also runs on Next.js, so it felt right for this project. In order to deploy it, I had to get a Postgres database running on [railway.app](https://railway.app), and then I just clicked umami's _Deploy to Vercel_ button, set some environment variables, and we were off to the races! Umami can track a large array of statistics, such as where people are from, and what devices they are using.

## The main implementation

The main implementation uses this tech stack:

    +----------------+  +---------------+
    |                |  |               |
    |  Next.js       +-->    Umami      |
    |  Multilink     |  |               |
    +--------+-------+  +------+--------+
             |                 |
    +--------v--------+--------v--------+
    |                 |                 |
    |              Vercel               |
    |                 |                 |
    +--------+--------+--------+--------+
             |                 |
             |                 |
    +--------v-------+  +------v--------+
    |                |  |               |
    | Airtable table |  |  Railway.app  |
    |                |  |               |
    +----------------+  +---------------+

(I made that drawing using [ASCIIFlow](https://asciiflow.com/#/))

As you can see, both apps run on Vercel and connect to their respective backend and the main Multilink app connects back to umami for analytics.

Not shown in the tech stack are the docs I had to make, as my friend isn't as technically savvy as I am. For those, I used [Notion](https://notion.so) and just shared the Notion link.

## Main Challenges

* Because this is a real person I'm building a website for, I had to include some security features, which meant I had to figure out .env files for Next.js.
* I also wanted to implement analytics, which meant I had to find a modern _and_ open-source analytics system.

## Wrap-up

Thanks for reading, this was a really fun project to make, and I'm still loving forestry for the post-writing!

Much love,

\- l3gacy
