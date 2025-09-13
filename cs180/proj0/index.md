---
layout: project
title: CS 180 Project 0 — Becoming Friends with Your Camera
subtitle: Selfie perspective, architectural compression, and a dolly zoom
last_updated: Sep 12, 2025
---

<section id="overview">
  <h2 id="overview">Overview</h2>
  <p>
    In this project, I examine how camera distance and focal length affect portraits, how changing viewpoint can exaggerate or compress architectural geometry, and how a dolly zoom keeps the subject size roughly constant while the background stretches or compresses.
  </p>
  <p>
    The key principle is that perspective depends on camera position. Zoom controls framing, but only moving the camera changes the relative sizes of near and far objects. Each part below isolates these effects by varying one factor at a time and matching framing when needed.
  </p>
</section>

<section id="part1">
  <h2 id="part1">Part 1 · Selfie: Wrong vs. Right</h2>
  <p>
    A close, wide‑angle selfie exaggerates nearby features (nose, forehead) and pushes ears and jawline outward due to perspective. Stepping back and using a longer focal length to match framing reduces distortion and produces a more natural portrait.
  </p>
  <div class="pair">
    <figure>
      <img class="fit selfie-sm" src="./assets/a_close.png?v=2" alt="Close up" />
      <figcaption>Close up, 25mm @ 50 cm</figcaption>
    </figure>
    <figure>
      <img class="fit selfie-sm" src="./assets/a_far.png?v=2" alt="Far" />
      <figcaption>Step back, 120mm @ 300 cm</figcaption>
    </figure>
  </div>
</section>

<section id="part2">
  <h2 id="part2">Part 2 · Architectural Perspective Compression</h2>
  <p>
    With buildings, near viewpoints exaggerate depth cues (stronger convergence of lines, foreground dominance). From farther away with a longer focal length (framing matched), the scene appears flatter and the background crowds in — the classic “compression” look.
  </p>

  <h3 id="b1">College of Letters &amp; Science</h3>
  <div class="pair" style="margin-bottom:10px;">
    <figure><img class="fit" src="./assets/b1_close.png?v=2" alt="L&S close" /><figcaption>Close up</figcaption></figure>
    <figure><img class="fit" src="./assets/b1_far.png?v=2" alt="L&S far" /><figcaption>Far away</figcaption></figure>
  </div>
  <p>
    Close: verticals converge more and the facade tapers noticeably. 
  </p>
  <p>
    Far: lines look more parallel and the structure reads flatter; distant background elements appear larger relative to the subject.
  </p>

  <h3 id="b2">J. Robert Oppenheimer’s Office</h3>
  <div class="pair">
    <figure><img class="fit" src="./assets/b2_close.png?v=2" alt="Oppenheimer close" /><figcaption>Close up</figcaption></figure>
    <figure><img class="fit" src="./assets/b2_far.png?v=2" alt="Oppenheimer far" /><figcaption>Far away</figcaption></figure>
  </div>
  <p>
    The same trend: perspective from the near position exaggerates depth; moving back compresses the scene so background elements seem to “move closer” to the subject.
  </p>
</section>

<section id="part3">
  <h2 id="part3">Part 3 · The Dolly Zoom</h2>
  <figure>
    <img class="fit" src="./assets/anim.gif?v=2" alt="Dolly zoom" />
    <figcaption>Constructed from 6 photos.</figcaption>
  </figure>
  <p>
    I captured a sequence by dollying forward while zooming out (and back while zooming in), keeping the subject size roughly fixed. Because perspective depends on distance, the background stretches when moving forward and compresses when moving back, creating the characteristic “vertigo” effect.
  </p>
</section>
