---
layout: post
title: "The Wattpad Romance - By The Numbers"
date: 2026-04-27
image:	
tags: research python claude_ai project romance smut fan-fiction books reading data statistics wattpad
---

> TL;DR, you can find all the data and simplified take-aways at [Wattpad Analysis](https://idleendeavor.com/wattpad-analysis.html). And yes, I am aware that AO3 is the go-to place for fan-fictions at the moment, but when I first had the idea; it was very much Wattpad. I might do the same data-analyis with AO3 at some point. (If you steal my idea, both sides of your pillow will be war for 7 years)

I've had this idea at the back of my head and later in my 'sometime' todo list for years at this point, never got around to doing it, and I've always been bummed about that.

However, having finished my last assessment project for the university year, which did include a lot of AI assistance in coding; I suddenly realised that AI would be a great way to automate a lot of the subjective aspects of this project which had always kept me from attemting to do it.

The idea when I first had it, in all honesty, was to analyse Wattpad fan-fictions to become the most attractive man possible. Since then my understanding of what 'attractiveness' is and what I 'want to be' have changed a lot, so the goal has shifted to just wanting to do the research to see what data it would come out with.

So I sat down and finally did the work, which took about 3 days to complete with a lot of back and forth with Claude, manual tweaking, graph building, and solving API implemetation and biling errors.

Anyway, you're here for the most common traits of the male and female characters. They are:

#### The Composite Heroine
She is 22 to 25 and working class, often a student, with little romantic experience to her name.
- **Age:**
22 to 25 (11/25)
- **Wealth:**
Working Class (7/25)
- **Build:**
petite / small (5/25)
- **Independence:**
Moderate (10/25)
- **Experience:**
Inexperienced (13/25)
- **Emotional maturity:**
Moderate (17/25)
- **Top traits in the prose:**
    - guarded (8)
    - fierce (7)
    - sassy (7)
    - resilient (7)
    - warm (6)
    - loyal (6)

#### The Composite Hero
He is 26 to 30 and very wealthy — tall, and almost always fiercely independent.
- **Age:**
26 to 30 (12/25)
- **Wealth:**
Very Wealthy (13/25)
- **Build:**
tall (9/25)
- **Independence:**
Fiercely Independent (22/25)
- **Experience:**
Experienced (16/25)
- **Emotional maturity:**
Moderate (13/25)
- **Top traits in the prose:**
    - broody (17)
    - cold (13)
    - protective (12)
    - possessive (7)
    - reserved (4)
    - controlling (4)

You can find a much more polished display of the full data at [Wattpad Analysis](https://idleendeavor.com/wattpad-analysis.html).

### The Nitty Gritty

I started by using Wattpad's built in list of the 25 most popular books from the Romance category (excluding foreign language entries and getting the 26th and 27th entries instead), then I _acquiring_ epub exports of the books and then wrote a python scropt which counted regex-matched vocabulary on roughly 40 different trait categories. This gave me the basic traits and a solid base to start off of. Here's all the code surrounding the vocabulary that was matched:


I've included some photos from the dashboard and terminal below.

![Python Script in Terminal](/images/wattpad-analysis-terminal.png)

![Claude API Dashboard](/images/wattpad-analysis-claude.png)

There are of course, some obvious caveats. 25 isn't a random sample, it's the top of a popularity list, which measures what gets read, not what gets written. AI labels were forced into a fixed enum to keep them comparable, which sanded off nuance. Personality clusters are pulled from free-text trait fields, so they reflect both the books' tendencies and the AI's vocabulary. The sample is also completely biased towards heterosexual romance as Wattpad classifies LGBTQIA+ stories under its own category (which I might explore separately at some point). Also, unlike Wattpad books from the past, modern ones don't seem to have detailed explanations of character appearances, due to this, most of the code around apearance matching amounted to no useable data.

That's about it, until next time!