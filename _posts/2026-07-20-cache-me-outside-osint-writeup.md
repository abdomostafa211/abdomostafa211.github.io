---
layout: post
title: "Cache Me Outside — TryHackMe OSINT Writeup"
date: 2026-07-20
categories: [osint, writeup]
tags: [osint, tryhackme, recon]
---

This is a walkthrough for the Cache Me Outside room on TryHackMe, an OSINT challenge.

## Background

Years after walking away from the scene, a retired hacker has left pieces of his identity scattered across the open internet.

At first glance, it looks like nothing more than a leaked conversation screenshot. But buried in that image is the first thread of a much larger trail. Public profiles, forgotten details, and small mistakes begin to connect into something more deliberate.

Someone wanted this person found.

## Your Assignment

You are an OSINT investigator tasked with identifying the retired hacker and tracing the clues he left behind.

Start with the conversation screenshot, follow his online presence, connect the exposed details, and use the final evidence to determine where the trail ends.

This challenge is basically a screenshot of a conversation between a retired hacker and his friend.

![chat](/assets/img/cache-me-outside/chat.png)

We don't have anything except this screenshot. In it, he says he quit hacking and started working out instead, and he sends his friend a link to his account on Komoot, which is a social platform for people who do sports and share challenges and achievements.

That's all the data we have. Now let's see how we get from just 4 messages to all the info we need.

## The Questions

- What is the retired hacker's full name?
- What email address did he accidentally expose?
- What is his phone number?
- In which city is he located?
- What is the name of the tram station where he got off on the 7th of May, 2026?

I'll go in the order I found the evidence, not the order of the questions.

## Step 1

First thing visible in the screenshot: he sent a link to his Komoot account. Komoot is just a regular social media site, but for athletes, where people share their achievements, races, and stuff like that.

Let's open the account.

www.komoot.com/user/5667624959835

![komoot-profile](/assets/img/cache-me-outside/komoot-profile.png)
<!-- IMAGE 2: his Komoot account -->

Nothing interesting in it, except he has his GitHub account linked.

Let's open it and move to the next step.

![github-profile](/assets/img/cache-me-outside/github-account.png)
<!-- IMAGE 3: his GitHub account -->

## Step 2

After digging around, there's nothing in the account.

But we can make use of the username since it looks distinctive — let's search for it.

![username-search-results](/assets/img/cache-me-outside/username-search-results.png)
<!-- IMAGE 4: searching for the username -->

We find an Instagram account with the same username. Let's open it.

![instagram-profile](/assets/img/cache-me-outside/instagram-profile.png)
<!-- IMAGE 5: his Instagram account -->

The account also has nothing in it, but there's a link to a Threads account.

Let's open it.

![Description](/assets/img/cache-me-outside/threads-profile.png)
<!-- IMAGE 6: his Threads account -->

Here we notice there are posts. The last post is a photo of a street.

Let's dig into it.

![street-photo](/assets/img/cache-me-outside/street-photo-original.png)
<!-- IMAGE 7: the photo -->

## Step 3

The photo doesn't show anything clear, so let's zoom in more.

![street-photo-zoomed](/assets/img/cache-me-outside/street-photo-zoomed.png)
<!-- IMAGE 8: zoomed street -->

We notice this store name:

IRIGATII.RO

.RO is the domain for Romania. So now we've narrowed it down and know the hacker is in Romania.

Let's search for the store name.

![store-search-result](/assets/img/cache-me-outside/store-search-result.png)
<!-- IMAGE 9: the store -->

There really is a store with this name. Digging around the listing a bit more, we get the address:

![store-location](/assets/img/cache-me-outside/store-location.png)
<!-- IMAGE 10: the listing with the address -->

Timisoara, Calea Buziasului no. 13,

So now we have the store's exact address inside Romania. Let's check it on Google Maps.

![google-maps-location](/assets/img/cache-me-outside/google-maps-location.png)
<!-- IMAGE 11: Google Maps -->

So now he's located in this exact spot.

## Back to the Questions

What is the retired hacker's full name? From the screenshot of his Komoot account, we know his name is Jim Lee.

In which city is he located? We confirmed it's Timișoara, from the store's address (Timisoara, Calea Buziasului no. 13).

What is the name of the tram station where he got off on the 7th of May, 2026?

The most important question. We currently know where he is, so let's zoom in more on his location.

![google-maps-location2](/assets/img/cache-me-outside/google-maps-location2.png)
<!-- IMAGE 12: his location -->

We find he's very close to a tram station called Ciarda Roșie (Bucla).

But the question wants the specific station he got off at. So let's go back to the photo he posted on his Threads account — what does the caption say?

"Just finished my last run before the big day, hopping on the tram for my well-deserved coffee at my favourite French supermarket."

This means the station he got off at is close to a French supermarket. So we need to find the most famous French supermarket chains in Romania and keep tracing along the tram line using Google Maps.

![Description](/assets/img/cache-me-outside/french-supermarket-in-romania.png)


<!-- IMAGE 13: tracing the tram line -->

After tracing the tram line and looking around it, we find the nearest well-known French supermarket

![Description](/assets/img/cache-me-outside/final-station.png)
<!-- IMAGE 14: the French supermarket found near the line -->

and so the station is Piața Gheorghe Domășneanu. That answers this question too.

## Step 4 (Email)

Two questions left:

- What email address did he accidentally expose?
- What is his phone number?

Let's take the first one — the email will take us back to digging in GitHub again.

After looping around the account a lot, there's nothing, the account is empty.

But sometimes instead of opening the Commit page normally on GitHub, you can add .patch to the end of the URL. GitHub will then show the commit as a plain text file (patch) instead of the normal site interface.

Inside this file you can sometimes find extra data about the person who made the commit, like their name or the email they used at the time of the commit. This is useful during Recon/OSINT because it can sometimes expose company or developer emails you can use to gather more info about the target.

Let's try it.

![Description](/assets/img/cache-me-outside/commit1.png)
<!-- IMAGE 15: the normal commit -->

After adding .patch

![Description](/assets/img/cache-me-outside/commit2.png)
<!-- IMAGE 16: after adding .patch -->

And now we reached his email: jimleepro1@gmail.com

## Step 5 (Phone Number)

Last question:

What is his phone number?

I tried a lot, with every piece of evidence we have, every method, long OSINT digging — none of it got me anywhere.

So I thought maybe his email could lead to something.

I opened his account — got nothing.

![Description](/assets/img/cache-me-outside/gmail.png)
<!-- IMAGE 17: Gmail -->

So why not just email him?

I tried sending him something, and here's the surprise: he has auto-reply turned on, and in the auto-reply he sends his phone number for people to contact him.

<!-- IMAGE 18: the auto-reply, part 1 -->
![Description](/assets/img/cache-me-outside/auto-reply.png)
<!-- IMAGE 19: the auto-reply, part 2 -->

And with that, we got the last answer:

+40 743 321 239

And that's the challenge fully solved.

Room link: https://tryhackme.com/room/cachemeoutside
