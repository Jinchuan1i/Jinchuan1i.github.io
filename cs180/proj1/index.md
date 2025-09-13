---
layout: project
title: CS180 — Project 1 (Jefferson Li)
subtitle: Colorizing the Prokudin-Gorskii photo collection
last_updated: Sep 12, 2025
---

<section id="overview">
  <h2 id="overview">Overview</h2>
  <p>
    This project colorizes grayscale glass plate negatives from the Prokudin‑Gorskii collection by aligning three channels
    (B, G, R) into a single RGB image. I use the green channel as reference and estimate integer‑pixel offsets for red and blue,
    using a single‑scale search for small JPGs and a coarse‑to‑fine image pyramid for high‑resolution TIFFs. Results and measured
    offsets are shown below.
  </p>
</section>

<section id="method">
  <h2 id="method">Method</h2>
  <p>
    For small images, I search a fixed window around the reference (G) for the best red/blue translation using the Sum of
    Squared Differences (SSD) over the overlapping region. For large images, I build an image pyramid and align from coarse to
    fine: estimate at the smallest scale in a small window, upsample offsets, then refine with a smaller search at the next scale.
  </p>
  <p>
    Practical details: I discard narrow borders to reduce edge artifacts and prefer the green channel as the reference because
    it balances texture and brightness. The final offsets are integer pixels per channel relative to green.
  </p>
</section>

<section id="results">
  <h2 id="results">Results</h2>
  <p class="muted">All images below are produced from <code>assets/images_out_green</code>. Captions list method and offsets (R: dx, dy; B: dx, dy) relative to G.</p>

  <section class="grid">
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/cathedral_aligned.jpg" alt="cathedral" />
        <figcaption>cathedral — method: single; R:(1, 7), B:(-2, -5)</figcaption>
      </figure>
    </article>
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/monastery_aligned.jpg" alt="monastery" />
        <figcaption>monastery — method: single; R:(1, 6), B:(-2, 3)</figcaption>
      </figure>
    </article>
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/tobolsk_aligned.jpg" alt="tobolsk" />
        <figcaption>tobolsk — method: single; R:(1, 4), B:(-3, -3)</figcaption>
      </figure>
    </article>

    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/church_aligned.jpg" alt="church" />
        <figcaption>church — method: pyramid; R:(-8, 33), B:(-4, -25)</figcaption>
      </figure>
    </article>
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/emir_aligned.jpg" alt="emir" />
        <figcaption>emir — method: pyramid; R:(17, 57), B:(-24, -49)</figcaption>
      </figure>
    </article>
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/harvesters_aligned.jpg" alt="harvesters" />
        <figcaption>harvesters — method: pyramid; R:(-3, 65), B:(-16, -59)</figcaption>
      </figure>
    </article>

    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/icon_aligned.jpg" alt="icon" />
        <figcaption>icon — method: pyramid; R:(5, 48), B:(-17, -41)</figcaption>
      </figure>
    </article>
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/italil_aligned.jpg" alt="italil" />
        <figcaption>italil — method: pyramid; R:(15, 38), B:(-21, -38)</figcaption>
      </figure>
    </article>
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/lastochikino_aligned.jpg" alt="lastochikino" />
        <figcaption>lastochikino — method: pyramid; R:(-7, 78), B:(2, 2)</figcaption>
      </figure>
    </article>

    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/lugano_aligned.jpg" alt="lugano" />
        <figcaption>lugano — method: pyramid; R:(-13, 52), B:(16, -41)</figcaption>
      </figure>
    </article>
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/melons_aligned.jpg" alt="melons" />
        <figcaption>melons — method: pyramid; R:(4, 96), B:(-10, -81)</figcaption>
      </figure>
    </article>
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/self_portrait_aligned.jpg" alt="self_portrait" />
        <figcaption>self_portrait — method: pyramid; R:(8, 98), B:(-29, -78)</figcaption>
      </figure>
    </article>

    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/siren_aligned.jpg" alt="siren" />
        <figcaption>siren — method: pyramid; R:(-18, 47), B:(6, -49)</figcaption>
      </figure>
    </article>
    <article class="card">
      <figure>
        <img class="fit" src="./assets/images_out_green/three_generations_aligned.jpg" alt="three_generations" />
        <figcaption>three_generations — method: pyramid; R:(-3, 58), B:(-13, -53)</figcaption>
      </figure>
    </article>
  </section>

  <section>
    <h3 id="emir-note">Emir: why green helps</h3>
    <div class="pair">
      <figure>
        <img class="fit" src="./assets/images_out_green/emir_aligned.jpg" alt="emir green reference" />
        <figcaption>Aligned using green as reference</figcaption>
      </figure>
      <figure>
        <img class="fit" src="./assets/emir_out_blue.jpg" alt="emir blue reference example" />
        <figcaption>Using blue reference can misalign due to low contrast</figcaption>
      </figure>
    </div>
  </section>

</section>

<section id="discussion">
  <h2 id="discussion">Discussion</h2>
  <p>
    Coarse‑to‑fine alignment is robust for high‑resolution plates where large displacements would be expensive to search at
    full scale. Using green as the anchor generally works well; challenging cases tend to have low‑contrast channels or strong
    brightness differences across plates. Further improvements could include gradient‑domain matching (NCC on edges) or subpixel
    refinement after integer alignment.
  </p>
  <p class="muted">
    Artifacts: residual color fringing near borders and moving objects; simple border cropping mitigates most.
  </p>
</section>

<section id="assets">
  <h2 id="assets">Assets</h2>
  <p>
    Offsets file: <a href="./assets/offsets.csv">assets/offsets.csv</a>. Notebook with implementation notes: <a href="./assets/RGB_Alignment_Clean.ipynb">assets/RGB_Alignment_Clean.ipynb</a>.
  </p>
</section>
