---
layout: post
title: "LeetCode Isn't the Job"
description: I hired two ML research assistants without a single puzzle question. Here's what worked.
tags: hiring interviews ML
date: 2026-03-25
---

I needed to hire two research assistants for a healthcare ML lab. The work involves messy clinical data where a wrong join or a leaked timestamp can quietly invalidate months of effort. I wanted an interview process that tested for that, not for puzzle-solving speed.

So I designed a realistic assessment: predict hospital readmission from two intentionally messy CSV files. Dirty dates, vitals recorded after discharge, extreme values, missing fields, a patient ID that appeared in one file but not the other. Candidates had 24 hours. AI tools were welcome. Understanding was not optional.

The funnel compressed fast. 73 eligible candidates. 45 after filtering for a referral. 35 submitted. 14 earned a live interview. Then 4.

The live round turned out to be the most informative step. Thirty minutes: walk me through your code, explain a decision, make a small change, debug something. The take-home showed who could ship runnable code. The live round showed who truly understood what they shipped.

The most common gap was not technical skill. It was the distance between what was submitted and what could be explained. Several candidates turned in polished work but struggled to make a targeted change or walk through a design choice. AI tools are powerful, but they work best for people who can evaluate and adapt the output.

The last four candidates were all technically strong. The difference came down to judgment: how they handled ambiguity, whether they thought about data leakage unprompted, how they communicated under pressure.

If you're hiring: consider a two-step process. A take-home that reflects real work, where candidates can use any tool they want, followed by a live interview where they walk through what they built. Let people use AI, copilots, whatever helps. Then ask them to explain it, change it, and own it. Make sure they know the live follow-up is coming.

If you're applying: you need to ace every step. If you can't ship runnable code, you won't make it past the take-home. If you can't explain and modify what you built, you won't make it past the live round. If any of these areas feel weak, practice before your next interview. Every step counts.
