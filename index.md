---
layout: default
title: Home
nav_order: 1
description: "This is project page of Behavior Atlas"
permalink: /
last_modified_date: 2020-07-15T17:54:08+0000
---

# Behavior Atlas: 
{: .fs-6 }

Behavior Atlas is a parallel, multi-layered framework for animal's motion feature decomposition, which provides an objective metric for mapping behavior into its feature space. We used a three-dimensional (3D) animal pose estimation technology that combines machine vision and machine learning to show that our framework can unsupervisedly decompose unconstrained animal behavior into behavioral phenotypes. 
{: .fs-6 .fw-300 }

![RUNOOB fig1](https://github.com/huangkang314/BehaviorAtlas/blob/master/imgs/fig1.svg "Figure1")

[Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on GitHub](https://github.com/huangkang314/HierBehaveTome){: .btn .fs-5 .mb-4 .mb-md-0 }

---
## Introdution
A fundamental issue in neuroscience is linking certain neural activity and its corresponding behavior [1–3]. Deciphering how neural networks generate behaviors, and how specific behaviors are encoded in the brain regions needs accurate and complementary measurement and quantification approaches [4,5]. Over the past few years, innovative advances in neuroscience have allowed us to monitor and manipulate [6,7] cell-type-specific neural circuits with precision and high-throughput [8–10]. It offers us unprecedented opportunities to study the circuit mechanisms behind behaviors. For instance, researchers have investigated the underlying neural circuits of spontaneous [17–19], innate [14–16], well-trained [11–13], and social behaviors [20–22] at circuitry or cellular resolution. However, due to the complexity and time variability of rodent behavior, comprehensively quantifying behavior to match accurate neural circuit recording and manipulation remains challenging.
Previous researchers addressed this challenge mainly from two aspects. The first aspect is behavioral features capturing. Conventional animal behavior experiments usually use a single camera top-view recording to capture the motion signal of behaving animals, leading to occlusions for the key body parts (e.g., paws) and very sensitive to viewpoint differences [23]. Fortunately, the recent emergence of novel Machine Learning (ML) toolboxes [24–26] has dramatically facilitated the animal pose estimation with multiple body parts. Thus, it enables us to study the animal kinematics more comprehensively and provides potential applications for capturing 3D animal movements. The second issue is decomposing continuous time-series data into understandable behavioral modules (e.g., walking, running, rearing). Previous studies on lower animals such as flies [27–31], zebrafishes [32–35] and C. elegans [36–39] took ML strategies and multivariate analysis to detect moment-to-moment actions. These leveraged approaches have demonstrated great applications, including behavior structure uncovering and modeling [36,40,41], neural circuits dissecting [42–44], brain-wide neural-behavioral mapping [31,45], etc. 
However, for mammals, their behavior is dynamic and high-dimensional. The dozens of degrees of freedom (DoF) [46] of the animal body lead to natural behavior with high variability in the temporal scale, and all possible combinations of motion primitives are exponential. Many ML-based open-source toolboxes [28] and commercial software did excellent works in feature engineering. Usually, they first compute per-frame features that refer to position, velocity, or appearance-based features. Then the sliding windows technology converts them into window features to reflect temporal context [47,48]. Although these approaches are effective for the identification of certain behaviors, once the dynamics of particular behaviors cannot be represented by window features, behavior recognition becomes problematic. A recently developed toolbox called MoSeq [49] took the idea that behavior is built out of a set of identifiable behavioral modules. Each module can be modeled as an AR-HMM (Autoregressive hidden Markov model). Therefore, the complexity and variability of behavior can be unsupervisedly decomposed into a limited number of stereotyped movement modules. 
Here, by combining the developed 3D motion capture system, we proposed an unsupervised general-purpose framework that aims to decompose animal behavior into metrizable movement modules. Inspired by the natural structure of animal behavior reported in previous theoretical studies, our framework involves a two-stage (pose and movement) behavior decomposition to reduce variation. We characterized the motion dynamics by applying the Dynamic Time Alignment Kernel (DTAK) method, which provides an objective metric to measure the similarity between movement sequences and constructs a feature space of spontaneous behavior. We demonstrated this framework to assess the spontaneous behavior of the transgenic animal disease model. By mapping mice behavior into their feature space without human supervision, we showed that the behavioral representations were highly consistent with genotypes.


## Getting started

### Dependencies

Just the Docs is built for [Jekyll](https://jekyllrb.com), a static site generator. View the [quick start guide](https://jekyllrb.com/docs/) for more information. Just the Docs requires no special plugins and can run on GitHub Pages' standard Jekyll compiler. The [Jekyll SEO Tag plugin](https://github.com/jekyll/jekyll-seo-tag) is included by default (no need to run any special installation) to inject SEO and open graph metadata on docs pages. For information on how to configure SEO and open graph metadata visit the [Jekyll SEO Tag usage guide](https://jekyll.github.io/jekyll-seo-tag/usage/).

### Quick start: Use as a GitHub Pages remote theme

1. Add Just the Docs to your Jekyll site's `_config.yml` as a [remote theme](https://blog.github.com/2017-11-29-use-any-theme-with-github-pages/)
```yaml
remote_theme: pmarsceill/just-the-docs
```
<small>You must have GitHub Pages enabled on your repo, one or more Markdown files, and a `_config.yml` file. [See an example repository](https://github.com/pmarsceill/jtd-remote)</small>

### Local installation: Use the gem-based theme

1. Install the Ruby Gem
```bash
$ gem install just-the-docs
```
```yaml
# .. or add it to your your Jekyll site’s Gemfile
gem "just-the-docs"
```
2. Add Just the Docs to your Jekyll site’s `_config.yml`
```yaml
theme: "just-the-docs"
```
3. _Optional:_ Initialize search data (creates `search-data.json`)
```bash
$ bundle exec just-the-docs rake search:init
```
3. Run you local Jekyll server
```bash
$ jekyll serve
```
```bash
# .. or if you're using a Gemfile (bundler)
$ bundle exec jekyll serve
```
4. Point your web browser to [http://localhost:4000](http://localhost:4000)

If you're hosting your site on GitHub Pages, [set up GitHub Pages and Jekyll locally](https://help.github.com/en/articles/setting-up-your-github-pages-site-locally-with-jekyll) so that you can more easily work in your development environment.

### Configure Just the Docs

- [See configuration options]({{ site.baseurl }}{% link docs/configuration.md %})

---

## About the project

Just the Docs is &copy; 2017-{{ "now" | date: "%Y" }} by [Patrick Marsceill](http://patrickmarsceill.com).

### License

Just the Docs is distributed by an [MIT license](https://github.com/pmarsceill/just-the-docs/tree/master/LICENSE.txt).

### Contributing

When contributing to this repository, please first discuss the change you wish to make via issue,
email, or any other method with the owners of this repository before making a change. Read more about becoming a contributor in [our GitHub repo](https://github.com/pmarsceill/just-the-docs#contributing).

#### Thank you to the contributors of Just the Docs!

<ul class="list-style-none">
{% for contributor in site.github.contributors %}
  <li class="d-inline-block mr-1">
     <a href="{{ contributor.html_url }}"><img src="{{ contributor.avatar_url }}" width="32" height="32" alt="{{ contributor.login }}"/></a>
  </li>
{% endfor %}
</ul>

### Code of Conduct

Just the Docs is committed to fostering a welcoming community.

[View our Code of Conduct](https://github.com/pmarsceill/just-the-docs/tree/master/CODE_OF_CONDUCT.md) on our GitHub repository.
