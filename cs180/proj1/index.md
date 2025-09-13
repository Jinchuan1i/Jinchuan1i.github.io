---
layout: project
title: CS180 Project 1 - Images of the Russian Empire
subtitle: Colorizing the Prokudin-Gorskii photo collection
last_updated: Sep 12, 2025
---

<section id="overview">
  <h2 id="overview">Overview</h2>
  <p>
    This project colorizes grayscale glass plate from the Prokudin‑Gorskii collection by aligning three channels
    (Blue, Green, Red) into a single RGB image. I use the green channel as reference and estimate integer‑pixel offsets for red and blue.
    For small JPGs, I align at a single scale. For large TIFFs, I use a coarse‑to‑fine image pyramid. Results and measured offsets
    are shown below.
  </p>
  <div class="pair" style="margin-top:10px;">
    <figure>
      <a href="./assets/example/monastery.jpg"><img class="fit" src="./assets/example/monastery.jpg" alt="Original glass plate" /></a>
      <figcaption>Original glass plate.</figcaption>
    </figure>
    <figure>
      <img class="fit" src="./assets/example/monastery_aligned.jpg" alt="Colorized Monastery" />
      <figcaption>Aligned and colorized result.</figcaption>
    </figure>
  </div>
</section>

<section id="method">
  <h2 id="method">Method</h2>
  <p>
    I use Normalized Cross‑Correlation (NCC) to score translations between channels. For each candidate offset (dx, dy), I compute
    correlation between standardized pixels and select the maximum. NCC is robust to global intensity changes and
    works well on these historical plates.
  </p>
  <p>
    For small JPGs, I search a fixed window around the reference (G) at full resolution. For large TIFFs, I build an image pyramid
    and align from coarse to fine: estimate at the smallest scale in a small window, upsample offsets, then refine at higher
    resolutions with smaller local windows. I crop borders slightly to avoid misleading edges.
  </p>
</section>

<section id="results">
  <h2 id="results">Results</h2>
  <p class="muted">Images are produced from <code>assets/images_out_green</code>. Captions list offsets (R: dx, dy; B: dx, dy) relative to G.</p>

  <h3 id="small">Small images (JPG)</h3>
  <section class="grid">
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/cathedral_aligned.jpg" alt="cathedral" />
      <figcaption>cathedral — R:(1, 7), B:(-2, -5)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/monastery_aligned.jpg" alt="monastery" />
      <figcaption>monastery — R:(1, 6), B:(-2, 3)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/tobolsk_aligned.jpg" alt="tobolsk" />
      <figcaption>tobolsk — R:(1, 4), B:(-3, -3)</figcaption>
    </figure></article>
  </section>

  <h3 id="large">Large images (TIFF)</h3>
  <section class="grid">
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/church_aligned.jpg" alt="church" />
      <figcaption>church — R:(-8, 33), B:(-4, -25)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/emir_aligned.jpg" alt="emir" />
      <figcaption>emir — R:(17, 57), B:(-24, -49)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/harvesters_aligned.jpg" alt="harvesters" />
      <figcaption>harvesters — R:(-3, 65), B:(-16, -59)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/icon_aligned.jpg" alt="icon" />
      <figcaption>icon — R:(5, 48), B:(-17, -41)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/italil_aligned.jpg" alt="italil" />
      <figcaption>italil — R:(15, 38), B:(-21, -38)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/lastochikino_aligned.jpg" alt="lastochikino" />
      <figcaption>lastochikino — R:(-7, 78), B:(2, 2)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/lugano_aligned.jpg" alt="lugano" />
      <figcaption>lugano — R:(-13, 52), B:(16, -41)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/melons_aligned.jpg" alt="melons" />
      <figcaption>melons — R:(4, 96), B:(-10, -81)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/self_portrait_aligned.jpg" alt="self_portrait" />
      <figcaption>self_portrait — R:(8, 98), B:(-29, -78)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/siren_aligned.jpg" alt="siren" />
      <figcaption>siren — R:(-18, 47), B:(6, -49)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/three_generations_aligned.jpg" alt="three_generations" />
      <figcaption>three_generations — R:(-3, 58), B:(-13, -53)</figcaption>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/Borodino's_church_aligned.jpg" alt="Borodino's_church" />
      <figcaption>Borodino's_church — R:(14, 59), B:(-25, -45)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/canal_aligned.jpg" alt="canal" />
      <figcaption>canal — R:(6, 81), B:(-20, -74)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/park_aligned.jpg" alt="park" />
      <figcaption>park — R:(0, 119), B:(-3, -44)</figcaption>
    </figure></article>
    <article class="card"><figure>
      <img class="fit" src="./assets/images_out_green/Vitebsk_aligned.jpg" alt="Vitebsk" />
      <figcaption>Vitebsk — R:(-11, 45), B:(7, -37)</figcaption>
    </figure></article>
  </section>

</section>

<section id="discussion">
  <h2 id="discussion">Discussion: Emir and robust alignment</h2>
  <p>
    Coarse‑to‑fine NCC works well overall, but Emir is particularly challenging. With the blue channel as reference, NCC can lock
    onto a strong yet incorrect correlation due to low contrast and color differences across plates, yielding a local maximum and
    visible color fringing. Using green as the reference and cropping noisy borders improves stability.
  </p>
  <div class="pair" style="margin-top:10px;">
    <figure>
      <img class="fit" src="./assets/emir/emir_aligned.jpg" alt="Emir aligned (green reference)" />
      <figcaption>Aligned to green — good facial alignment.</figcaption>
    </figure>
    <figure>
      <img class="fit" src="./assets/emir/emir_out_blue.jpg" alt="Emir misaligned (blue reference)" />
      <figcaption>Aligned to blue — local maximum. strong color fringes.</figcaption>
    </figure>
  </div>
  <p>
    A robustness trick is to run NCC on Sobel gradient magnitude rather than raw intensities: compute horizontal/vertical
    derivatives, take the magnitude, and normalize each patch before correlation. This emphasizes shared structure (edges and
    contours) and deemphasizes lighting differences and flat regions, helping escape the bad maximum on Emir. Combined with border
    cropping and a pyramid search, this yields reliable alignment.
  </p>
</section>

<section id="assets">
  <h2 id="assets">Assets</h2>
  <p>
    Offsets file: <a href="./assets/offsets.csv">assets/offsets.csv</a>. Browse and download larger results here: <a href="./assets/">assets/</a>.
  </p>
</section>
