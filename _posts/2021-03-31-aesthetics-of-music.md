---
layout: post
title: "Notes From a Conversion About the Aesthetics of Music"
description: "A mathematical theory of the aesthetics of music"
date: 2021-03-31
giscus_comments: true
toc:
  sidebar: left
tags: mathematics
citation: true
---

Notes from a conversation with a friend, during a long car ride, about how to evaluate music.

## Theory

**Feels**. The primary goal of music is to evoke an emotional (in the broadest possible sense) response. Music may have ulterior motives of communication or persuasion. Thus, better songs evoke more powerful emotional responses.

**Emotional relativism**. There is no true emotional response to a music. What a human feels listening to a song, depends on their ear, experience, and cultural conditioning. For example, in Western music major chords sound happy while minor chords sound sad, but this is not universal across human cultures.

**Average**. Instead, we use the averaged emotional response (AER) from a proper listen of a recorded version of a song (for consistency) across a population at a given time.

**L1 norm**. The AER is a signal $f\colon \text{Emotion Space} \to [0, \infty)$. We can take the L1 norm of the signal by weighting the intensity with a super-linear function $w\colon [0, \infty) \to [0, \infty)$. For example, $w(x) = x \log(x)$,

$$
\| f \|_1 = \int_{\text{Emotion Space}} w(f(e)) \mathop{de}
$$

A greater L1 norm is a better song.

## Corollaries

- More intense emotions are privileged over less intense emotions. A song which evokes 10 happy is better than a song that evokes 5 happy
- Emotional complexity is privileged over emotional simplicity. A song which evokes 10 happy and 5 sad (bittersweet) is better than a song that evokes 10 happy.
- Misinterpreted songs are worse than widely understood songs. For example, Born in the USA can be interpreted as 10 patriotic or 10 anti-war. The AER is 5 patriotic, 5 anti-war. Then Born in the USA has a lesser L1 norm than a song whose AER is solely 10 happy due to the super linear weighting.
