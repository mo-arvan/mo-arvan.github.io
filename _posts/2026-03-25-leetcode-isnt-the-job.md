---
layout: post
title: "How I Actually Hire"
description: I hired two ML research assistants without a single puzzle question. Here's what worked.
tags: hiring interviews ML
date: 2026-03-25
giscus_comments: true
---

I needed to hire two research assistants for a healthcare ML lab. The work involves messy clinical data where a wrong join or a leaked timestamp can quietly invalidate months of effort. I wanted an interview process that tested for that, not for puzzle-solving speed.

I designed a two-step process. First, a take-home: predict hospital readmission from two intentionally messy CSV files. Dirty dates, vitals recorded after discharge, extreme values, missing fields, a patient ID that appeared in one file but not the other. Candidates had 24 hours. AI tools were welcome. Understanding was not optional.

Second, a 30-minute live interview. Walk me through your code, explain a decision, make a small change, debug something.

73 candidates were eligible. 45 after filtering for a referral. 35 submitted. 14 earned the live round. 4 could confidently walk through their own code.

The take-home showed who could ship runnable work. The live round showed who understood what they shipped. That turned out to be the most informative step in the entire process.

The most common gap was not technical skill. It was the distance between what was submitted and what could be explained. Several candidates turned in polished work but struggled to make a targeted change or walk through a design choice. AI tools are powerful, and they work best for people who can evaluate and adapt the output.

The last four candidates were all technically strong. The difference came down to judgment: how they handled ambiguity, whether they thought about data leakage unprompted, how they communicated under pressure.

If you're hiring, consider something similar. A take-home that reflects real work, where candidates can use any tool they want, followed by a live interview where they walk through what they built. Make sure they know the follow-up is coming.

If you're applying, every step counts. Practice shipping runnable code. Practice explaining what you built and why. Practice making small, targeted changes under mild pressure. These are the skills that separate candidates in the final round.
