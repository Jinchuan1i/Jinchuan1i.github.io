---
layout: project
title: CS180 Project 1 - Images of the Russian Empire
subtitle: Colorizing the Prokudin-Gorskii photo collection
last_updated: Sep 12, 2025
---

<section id="overview">
  <h2 id="overview">Overview</h2>
  <p>
    This project colorizes grayscale glass plate negatives from the Prokudin‑Gorskii collection by aligning three channels
    (B, G, R) into a single RGB image. I use the green channel as reference and estimate integer‑pixel offsets for red and blue.
    For small JPGs I align at a single scale; for large TIFFs I use a coarse‑to‑fine image pyramid. Results and measured offsets
    are shown below.
  </p>
  <div class="pair" style="margin-top:10px;">
    <figure>
      <a href="./assets/example/church.tif"><img class="fit" src="./assets/example/church.tif" alt="Original glass plate (TIF)" /></a>
      <figcaption>Original glass plate (TIF). Some browsers may not display TIF inline; click to download.</figcaption>
    </figure>
    <figure>
      <img class="fit" src="./assets/example/church_aligned.jpg" alt="Colorized church" />
      <figcaption>Aligned and colorized result.</figcaption>
    </figure>
  </div>
</section>

<section id="method">
  <h2 id="method">Method</h2>
  <p>
    I use Normalized Cross‑Correlation (NCC) to score translations between channels. For each candidate offset (dx, dy), I compute
    correlation between zero‑mean, unit‑variance patches and select the maximum. NCC is robust to global intensity changes and
    works well on these historical plates.
  </p>
  <p>
    For small JPGs, I search a fixed window around the reference (G) at full resolution. For large TIFFs, I build an image pyramid
    and align from coarse to fine: estimate at the smallest scale in a small window, upsample offsets, then refine at higher
    resolutions with smaller local windows. I crop borders slightly to avoid misleading edges.
  </p>
  <p>
    To further reduce sensitivity to illumination and fine noise, I optionally run NCC on Sobel gradient magnitude images — this
    emphasizes structure and edges over raw intensities and helps avoid local maxima, especially on challenging images like Emir.
  </p>
</section>

<section id="results">
  <h2 id="results">Results</h2>
  <p class="muted">Images are produced from <code>assets/images_out_green</code>. Captions list offsets (R: dx, dy; B: dx, dy) relative to G.</p>

  <h3 id="small">Small images (JPG)</h3>
  <section class="grid grid-2">
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
  <section class="grid grid-2">
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
    </figure></article>
  </section>

  <section>
    <h3 id="emir-note">Emir: local maxima and robust matching</h3>
    <p>
      Emir is particularly challenging: NCC against the blue reference can get stuck in a local maximum due to low contrast and
      color differences. Two fixes worked well for me: (1) use green as the reference and crop wider borders to ignore noisy edges;
      (2) compute NCC on Sobel gradient magnitude to emphasize structure over intensity.
    </p>
    <div class="pair">
      <figure>
        <div class="crop zoom2"><img src="./assets/images_out_green/emir_aligned.jpg" alt="emir aligned (green ref)" /></div>
        <figcaption>Aligned to green, cropped borders, NCC on gradients.</figcaption>
      </figure>
      <figure>
        <div class="crop zoom2"><img src="./assets/emir_out_blue.jpg" alt="emir misaligned (blue ref)" /></div>
        <figcaption>Blue reference can converge to a poor local maximum.</figcaption>
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
    Notebook with implementation notes: <a href="./assets/RGB_Alignment_Clean.ipynb">assets/RGB_Alignment_Clean.ipynb</a>.
  </p>
</section>
