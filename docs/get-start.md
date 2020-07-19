---
layout: default
title: Getting started
nav_order: 2
---

# Getting started
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Prerequisites

**Hardware:** 
- 8GB Minimum RAM for single experimental data (~ 20mins); For batch analysis of large amount of data, recommended 64GB or more;

**Software:** 
- MATLAB 2016 or higher version;

### Download codes
- a. Clone or download our repository [Behavior-Atlas](https://github.com/huangkang314/Behavior-Atlas) to local, and unZip it;
- b. Download [Feng Zhou's](http://www.f-zhou.com/) [aca](https://github.com/zhfe99/aca) code, unZip the code to the folder `Behavior-Atlas\lib\`;
- c. Make sure your Matlab has the UMAP toolbox, if not, please download(https://fr.mathworks.com/matlabcentral/fileexchange/71902-uniform-manifold-approximation-and-projection-umap) it and include it to your Matlab path.

### Download demo data
Go to [Data Resource](https://behavioratlas.netlify.app/docs/data-resource/) Download the demo dataset and its corresponding video. 


### Install
- Run `make.m` to compile all C++ files;
- Run `test.m` to verify the installation.






