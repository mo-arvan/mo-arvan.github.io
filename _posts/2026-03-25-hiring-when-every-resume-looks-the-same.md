---
layout: post
title: "Hiring When Every Resume Looks the Same"
description: 73 applicants, two positions, and every candidate had access to AI.
tags: hiring interviews ML AI
date: 2026-03-25
giscus_comments: true
---

73 people applied for two research assistant positions in my center. Most of their resumes looked the same. Everyone knew Python. Everyone listed machine learning, NLP, and deep learning. Everyone had a project or two on GitHub. Reading 73 applications where every candidate claims fluency in everything is not a screening process. It's noise.

And that's before you account for AI tools. Every one of these candidates had access to AI tools. The floor on what someone can produce has risen. The traditional approach (screen resumes, then run candidates through four or five rounds of interviews to figure out what's real) doesn't scale when the resumes all look the same and the submitted work might not be theirs.

I wasn't evaluating anyone's ability to generate code. I was evaluating critical judgment. I needed people who could work in an environment where the hardest part isn't writing code. It's deciding what to do when the data is ambiguous, the requirements are underspecified, and a quiet mistake compounds for months before anyone notices. That's not something you can evaluate with a resume screen or a puzzle question.

So I designed something different.

## Messy data, real decisions, blitz interview

I gave candidates two intentionally messy CSV files and a prediction task: hospital readmission. Dirty dates. Vitals recorded after discharge. Extreme values. Missing fields. A patient ID that appeared in one file but not the other. 24 hours. AI tools welcome, as long as candidates could take full ownership of what they submitted.

The point wasn't the prediction. It was the mess. Every dataset had decisions buried in it. What to do about the post-discharge vitals. How to handle the mismatched IDs. Whether to impute or drop. There was no right answer to most of these. I wanted to see how candidates navigated that.

I code-reviewed every submission. I wasn't checking whether scripts ran. I was reading for judgment: did they notice the leakage? Did they document their choices? Did they handle the ambiguity or pretend it wasn't there?

## The funnel: 73 to 4

73 eligible. 45 after requiring a referral. 35 submitted. 14 showed enough judgment in the code review to earn a live round.

Then 4.

The live interview was 30 minutes, and the questioning was targeted at ownership. Walk me through your code. Why did you make this choice? Now make a small change.

This was the most informative step in the entire process. The most significant factor in my decisions was the gap between a candidate's stated proficiency and their ability to solve problems independently in the live round. Several candidates turned in polished, well-structured work and then couldn't walk through a design choice or make a targeted modification to their own code.

The work looked like theirs. The understanding wasn't.

## The real filter

The take-home filtered for judgment. The blitz filtered for something more basic: did they actually know what they submitted? Some candidates who turned in clean, well-reasoned code couldn't explain basic concepts in conversation. Some couldn't write a few lines of Python to filter a dataframe when asked to make a small change live.

The ownership gap matters because the work is research. A pipeline the author doesn't understand is a finding that can't be trusted. A silent error isn't a bug you patch next sprint. It's months of wasted work or a wrong conclusion that gets published. The accountability is higher, and there's no shortcut around understanding what your code actually does.

The difference isn't between people who use AI tools and people who don't. It's between people who recognize the limitations of these tools and work around them, and people who follow their output blindly.

A [Harvard/BCG study](https://www.oneusefulthing.org/p/centaurs-and-cyborgs-on-the-jagged) found that when AI gave plausible but wrong answers, consultants who trusted it without critical judgment performed worse than those with no AI at all. The ones who recognized the limits were far more productive. That's who I was hiring for.
