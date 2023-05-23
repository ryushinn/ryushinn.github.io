---
layout: default
title: Learning to Learn and Sample BRDFs
---

<!-- Title -->
<!-- Venue -->
<!-- Authors -->
<!-- Institutions -->

<div class="publication-banner">
<h1><b>Learning to Learn and Sample BRDFs</b></h1>
<h4><em>Eurographics 2023</em></h4>
<br>
<h4>
<a href="https://ryushinn.github.io/">Chen Liu</a>, <a href="https://mfischer-ucl.github.io/">Michael Fischer</a>, <a href="https://www.homepages.ucl.ac.uk/~ucactri/">Tobias Ritschel</a>
</h4>
<h4>
<a href="https://www.ucl.ac.uk/">University College London</a>
</h4>
</div>

<!-- Resources -->

---

<div class="publication-resources">
<p>
    <!-- PDF -->
    <a type="button" class="btn btn-dark"
        href="https://arxiv.org/pdf/2210.03510.pdf">
        <i class="fas fa-file-pdf"></i>
        PDF
    </a>
    <!-- Video -->

    <!-- Slides -->
    <a type="button" class="btn btn-dark"
        href="{{ 'slide_metasampling.pdf' | prepend: '/assets/publications/metasampling/' | relative_url }}">
        <i class="fas fa-file-powerpoint"></i>
        Slides
    </a>

    <!-- Code Repo -->
    <a type="button" class="btn btn-dark"
        href="https://github.com/ryushinn/meta-sampling">
        <i class="fab fa-github"></i>
        Code
    </a>

    <!-- Supplemental -->
    <a type="button" class="btn btn-dark"
        href="{{ 'liu2023learning_supplemental.zip' | prepend: '/assets/publications/metasampling/' | relative_url }}">
        <i class="fas fa-paperclip"></i>
        Suppl.
    </a>

    <!-- ArXiv -->
    <a href="https://arxiv.org/abs/2210.03510"
        type="button" class="btn btn-dark">
        <i class="ai ai-arxiv"></i>
        arXiv
    </a>

    <!-- Publisher Version -->
    <a href="https://doi.org/10.1111/cgf.14754"
        type="button" class="btn btn-dark">
        <i class="fa-solid fa-right-from-bracket"></i>
        Publisher
    </a>

</p>
</div>

---
<!-- Others -->

<!-- Teaser -->
<div class="row">
    <div class="col-12 text-center">
        <figure class="figure">
        <img
            src="{{ 'Teaser.png' | prepend: '/assets/publications/metasampling/' | relative_url }}"
            class="figure-img img-fluid shadow-3 mb-3"
            alt="meta-sampling_teaser"
        />
        <figcaption class="figure-caption">Equal-time comparison between a neural BRDF model fitted without meta-learning (top), fitted with meta-learning (second row) and fitted with our meta-sampling (third row).</figcaption>
        </figure>
    </div>
</div>

## Abstract

We propose a method to accelerate the joint process of physically acquiring and learning neural BRDF models.
While BRDF learning alone can be accelerated by meta-learning, acquisition remains slow as it relies on a mechanical process.
We show that meta-learning can be extended to optimize the physical sampling pattern, too.
After our method has been meta-trained for a set of fully-sampled BRDFs, it is able to quickly train on new BRDFs with up to five orders of magnitude fewer physical acquisition samples at similar quality.
Our approach also extends to other linear and non-linear BRDF models, which we show in an extensive evaluation.

## Algorithm

<div class="row">

<div markdown="1" class="col-md-5 col-12">

In the right is our proposed method, which meta-trains the locations of samples until they become the most informative.

The <span style="color:orange;">orange</span> snippet meta-trains the model parameters, and the <span style="color:blue;">blue</span> snippet meta-trains the sample locations.

- <span style="font-variant: small-caps;">**Learn**</span>:
Run SGD fitting with the given model parameters and samples on one task, in a differentiable way.

- <span style="font-variant: small-caps;">**Evaluate**</span>:
Evaluate the given model parameters over one task, in a differentiable way.

</div>

<div class="col-md-7 col-12 text-center">
    <figure class="figure">
    <img
        src="{{ 'algorithm.png' | prepend: '/assets/publications/metasampling/' | relative_url }}"
        class="figure-img img-fluid mb-3"
        alt="algo"
    />
    <figcaption class="figure-caption">A short version of the algorithm. <br>
    Check the paper for the full explanation.
    </figcaption>
    </figure>
</div>

</div>

## Exemplary Results

### Learned patterns

<div class="row">
<div class="col-12 text-center">
    <figure class="figure">
    <img
        src="{{ 'Pattern.png' | prepend: '/assets/publications/metasampling/' | relative_url }}"
        class="figure-img img-fluid mb-3"
        alt="diffuse"
    />
    <figcaption class="figure-caption">2D projections <span markdown="1">($$\theta_d-\theta_h$$)</span> of our meta-sampling patterns at n = 8 for all models. <br> The NJR5 pattern is also included for reference.
    </figcaption>
    </figure>
</div>
</div>

These samples above are deemed as optimal for BRDF acquisition by our method.

We provide all optimal samples (from `n=1` to `n=1024`) trained by ourselves, for off-shelf usages and to people who don't want to train again. You can download them at [the code repo](https://github.com/ryushinn/meta-sampling#data).

### Same # of samples

<div class="row justify-content-center">

<div class="col-md-6 col-8 text-center">
    <figure class="figure">
    <img
        src="{{ 'MethodsModels_8samples_diff.png' | prepend: '/assets/publications/metasampling/' | relative_url }}"
        class="figure-img img-fluid mb-3"
        alt="diffuse"
    />
    <figcaption class="figure-caption">Reconstructions by 8 samples for <span markdown="1">`blue-rubber`</span> (diffuse)
    </figcaption>
    </figure>
</div>

<div class="col-md-6 col-8 text-center">
    <figure class="figure">
    <img
        src="{{ 'MethodsModels_8samples_glos.png' | prepend: '/assets/publications/metasampling/' | relative_url }}"
        class="figure-img img-fluid mb-3"
        alt="glossy"
    />
    <figcaption class="figure-caption">Reconstructions by 32 samples for <span markdown="1">`silver-paint`</span> (glossy)
    </figcaption>
    </figure>
</div>

</div>

### Increasing # of samples

<div class="col-12 text-center">
    <figure class="figure">
    <img
        src="{{ 'IncreasingSamples.png' | prepend: '/assets/publications/metasampling/' | relative_url }}"
        class="figure-img img-fluid mb-3"
        alt="glossy"
    />
    <figcaption class="figure-caption">results of using our proposed meta-sampling for the training of each model (vertical) on the BRDF <span markdown="1">`two-layer-gold`</span> for an increasing number of samples (horizontal).
    </figcaption>
    </figure>
</div>

## Acknowledgement

We appreciate valuable comments from Vlastimil Havran, Stavros Diolatzis, and Gilles Rainer. We also thank Meta Reality Labs for funding a part of this project.

## Citation

```bibtex
@article{liu2022learning,
  title={Learning to Learn and Sample BRDFs},
  author={Liu, Chen and Fischer, Michael and Ritschel, Tobias},
  journal={arXiv preprint arXiv:2210.03510},
  year={2022}
}
```
