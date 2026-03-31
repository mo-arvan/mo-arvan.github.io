---
layout: distill
title: "A 75-Word Limit Shouldn't Take Five Tries"
description: We asked a language model to answer patient questions under simple constraints. It matched the word count. It didn't match the writing.
tags: LLM NLP constraints clinical-AI
date: 2026-03-31
giscus_comments: true

authors:
  - name: Mohammad Arvan

---

Ask a language model to answer a patient's question from their medical record. Simple enough. Now add constraints: ground every claim in a specific sentence from the clinical note. Keep it under 75 words. Write in third person. Use past tense for events during hospitalization, present tense for prognosis. Match the style of a clinician writing for a lay reader.

Each of these instructions is straightforward on its own. Stack them together and the model starts failing in ways that standard evaluation metrics don't capture.

## The 75-word problem

We built a system for the ArchEHR-QA 2026 shared task, which evaluates grounded question answering from electronic health records. The task requires a model to identify which sentences in a clinical note support the answer, generate a natural-language response under 75 words, and align each answer sentence to its evidence.

The simplest constraint was the hardest to enforce. On the development set, 85.9% of outputs met all format and length requirements on the first attempt. On the test set, that dropped to 64.3%. Word count violations accounted for 95% of all test errors. Not citation errors. Not format errors. The model couldn't count to 75.

We fixed this with an iterative correction loop: when an output violated a constraint, we told the model exactly what was wrong and let it retry, up to five times. The loop achieved 100% compliance on both sets. But the fact that it was necessary at all is the point. A model that needs five attempts to meet a word limit it was given in the original prompt is not following instructions. It's being corrected into compliance.

{% include figure.liquid path="assets/img/post_archehr/error_breakdown.png" caption="Word count violations accounted for 88% of all errors across 1,171 cases. The model handled citations, schema, and format. It couldn't count." zoomable=true %}

{% include figure.liquid path="assets/img/post_archehr/compliance_funnel.png" caption="Cumulative compliance across correction attempts. The model reached 100% compliance, but needed up to five tries to get there." zoomable=true %}

## What the metrics missed

The compliance loop solved the format problem. It did not solve the style problem.

Our system matched clinician-authored answers on word count (72.7 vs. 73.5) and sentence count (4.45 vs. 4.75). Neither difference was statistically significant. By the most obvious measures, the outputs looked like clinician writing.

They weren't. We computed 45 linguistic features across six categories and compared model outputs to clinician references<d-footnote>We used paired Wilcoxon signed-rank tests with Benjamini-Hochberg correction for multiple comparisons across 45 features.</d-footnote>. Eight features diverged significantly. The model wrote text that was 3.2 Flesch-Kincaid grade levels harder to read<d-footnote>Flesch-Kincaid Grade Level estimates the US school grade needed to understand a text. The clinician reference averaged grade 10.7. The model averaged 13.9, roughly college level.</d-footnote>. It used longer words, fewer function words, and produced denser, more noun-heavy prose. The writing read like a medical textbook, not like a clinician explaining a result to a patient.

These answers are for patients. A response that is factually correct, properly grounded, and within the word limit can still fail its purpose if the patient can't understand it. The standard evaluation metrics (BLEU, ROUGE, BERTScore, MEDCON) did not flag this gap. Length matched. Style didn't.

## More instructions, worse results

The natural question is why. The model was explicitly instructed to write in plain language. It was given style guidance, tense rules, and a word limit. Why did it follow the word limit (eventually) but not the register?

Research on instruction-following degradation offers a partial answer. When models are given multiple competing objectives in a single prompt, performance on individual constraints drops as the total number increases. Work on [humanization attacks](https://arxiv.org/abs/2401.12926) and [detection evasion](https://arxiv.org/abs/2310.02417) shows the same pattern: models can be steered to match a target style, but not while simultaneously maintaining grounding and format compliance.

Some researchers call this "cognitive overload." LLMs do not have cognition. What happens is better described as constraint interference: the model satisfies whichever instruction is most explicitly reinforced and underperforms on the rest. Word count is easy to verify and correct. Register is not.

## You can split the task. That doesn't solve the problem.

We tested whether separating the competing objectives would help. After the submission deadline, we built a three-step rewrite variant: (1) generate an unconstrained answer grounded in the evidence, (2) rewrite it for clinical register, (3) enforce the word limit as a separate call.

{% include figure.liquid path="assets/img/post_archehr/linguistic_radar.png" caption="Linguistic profiles for the two-step (submitted) and three-step (post-deadline) pipelines, normalized to the clinician reference (unit circle). The three-step pipeline traces closer to the clinician on nearly every dimension." zoomable=true %}

The decomposed pipeline reduced the linguistic distance to the clinician reference from 0.519 to 0.381 and improved the automatic evaluation score by approximately two points. Readability moved closer to clinician levels. The tradeoff: 9.5x latency.

But this is a band-aid, not a fix. You can always split tasks up. You can always add correction loops, rewrite passes, and verification steps. At some point you're not using a language model to generate answers. You're building a scaffold around a language model to compensate for the fact that it can't follow basic instructions reliably.

## The error tolerance problem

Our system achieved 100% compliance after correction. That sounds like success. But 100% compliance after five attempts is not the same as 100% compliance on the first attempt. The first number means the scaffold works. The second number means the model works. On the test set, the model's first-attempt compliance was 64.3%. That is the real number.

In clinical settings, the tolerance for errors approaches zero. If a system cannot demonstrate near-zero error rates on simple, verifiable constraints like word count, it cannot be trusted with harder, less verifiable ones like reading level, tone, and clinical accuracy. The easy constraints are the lower bound. If the model fails there, everything above it is suspect.

The workarounds exist. Decompose, correct, verify, repeat. Each layer of scaffolding is an admission that the model alone is not reliable enough. For clinical applications, that admission matters.
