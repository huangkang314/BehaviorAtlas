---
layout: default
title: Home
nav_order: 1
description: "This is project page of Behavior Atlas"
permalink: /
last_modified_date: 2020-07-15T17:54:08+0000
---

# Behavior Atlas: 
{: .fs-9 }

[Get started now](https://behavioratlas.netlify.app/docs/get-start/){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on GitHub](https://github.com/huangkang314/HierBehaveTome){: .btn .fs-5 .mb-4 .mb-md-0 }

## Introdution
Behavior Atlas is a spatio-temporal decomposition framework for automatically detecting behavioral phenotypes. It receives 3D/2D continuous multidimensional motion features data input, and unsupervisedly decompose it into understandable behavioral modules/movements (e.g., walking, running, rearing). Our framework emphasizes the extraction of the temporal dynamics of movements. Without making model assumptions, similar movements with various time durations and temporal variability can be efficiently detected. Besides the decomposition, the constructed self-similarity matrix of these movement segments describes the structure of involved movements. Further dimensionality reduction and visualization enable us construct the feature space of behavior. This helps us study the evolution of movement sequences for higher-order behavior and behavioral state transition caused by neural activity. 

## Features
### 1. The real 3D reconstruction of animal poses with a high signal-to-noise ratio 
- a. Capturing Image streams from four cameras with different 2D views; 
- b. Using <a href="https://github.com/DeepLabCut/DeepLabCut" target="_blank">DeepLabCut</a> (DLC) to track animal body parts and generate 2D skeletal trajectories separately (color-coded traces); 
- c. Reconstructing 3D body skeleton by integrating these four data streams (based on <a href="https://github.com/SwathiSheshadri/pose3d" target="_blank">pose3d</a>).

<video width="100%" height = "auto" controls="controls">
  <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video1-3D_Capture_and_recons_demo.mp4"></source>
  Your browser does not support the video tag.
</video>

Video1 | 3D reconstruction demo video, Download this video <a href="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video1-3D_Capture_and_recons_demo.mp4" target="_blank">Video1-3D_Capture_and_recons_demo.mp4 (11.6MB)</a>

![The pipeline of 3D animal skeletal reconstruction](https://behavioratlas.netlify.app/imgs/3Dpipeline.svg "Figure1") 

Figure1 | The pipeline of 3D animal skeletal reconstruction. 

![representative (900s) mouse body tracking trace data showing with 48 data vectors obtained by 3D reconstruction](https://behavioratlas.netlify.app/imgs/3DskeletalTrace.png "Figure2") 

Figure2 | Representative (900s) mouse body tracking trace data showing with 48 data vectors obtained by 3D reconstruction. 

### 2. Parallel and two-layer framework for motion feature decomposition.

There are many similar previous works such as <a href="https://github.com/gordonberman/MotionMapper" target="_blank">MotionMapper</a>, <a href="http://datta.hms.harvard.edu/research/behavioral-analysis" target="_blank">Moseq</a> were used to detect stereotyped movement modules on flies or mice. Our framework focus on address the high-dimensionality and large temporal variability of rodent behavior. we adopted a parallel motion decomposition strategy following the natural characteristics of animal motion. That is, two-layer dynamic temporal decomposition is performed on the continuous animal skeleton postural data to obtain Non-locomotor movement (NM) space. Finally, together with locomotion dimension, unsupervised clustering is used to reveal the structure of behavior.

![Spatio-temporal decomposition framework for animal behavior analysis fig1](https://behavioratlas.netlify.app/imgs/fig1.svg "Figure3")

Figure3 | Spatio-temporal decomposition framework for animal behavior analysis. 


### 3. Mapping Mouse Movements with Low-Dimensional Embeddings and Unsupervised Clustering

We demonstrate our framework in 15-minute experimental data collected in a featureless circular open-filed. Thus, we obtained 11 types (determined by <a href="https://pubmed.ncbi.nlm.nih.gov/27818791" target="_blank">Bayesian Information Criterion</a> ) of movement. 

<video width="100%" height = "auto" controls="controls">
  <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video2-decomposition_demo.mp4"></source>
</video>

Video2 | Decomposition demo of 15-minute experimental data collected in a featureless circular open-filed <a href="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video2-decomposition_demo.mp4" target="_blank">Video2-decomposition_demo.mp4 (68.2MB)</a> (CQI: Clustering Quality Index helps us determine the stereotyped/non-stereotyped movements. CQI is evaluated by integrated  the intra-cluster and inter-cluster correlation coefficients. Larger CQI indicates more stereotyped movement segment)

We examined the video clips in each group, post-hoc manually labeled annotated as running, trotting, stepping, sniffing, rising, right turning, up stretching, falling, left turning, walking.   

<table class="table">
  <tbody>
      <tr>
        <th>Up stretching</th>
        <th>Running</th>
        <th>Rising</th>
        <th>Sniffing</th>
      </tr>
      <tr>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/1-up_stretching.mp4"></source>
          </video>
        </td>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/2-running.mp4"></source>
          </video>
        </td>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/3-rising.mp4"></source>
          </video>
        </td>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/4-sniffing.mp4"></source>
          </video>
        </td>
      </tr>
      <tr>
        <th>Stepping</th>
        <th>Falling</th>
        <th>Diving</th>
        <th>Right turning</th>
      </tr>
      <tr>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/5-diving.mp4"></source>
          </video>
        </td>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/6-right_turning.mp4"></source>
          </video>
        </td>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/7-stepping.mp4"></source>
          </video>
        </td>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/8-falling.mp4"></source>
          </video>
        </td>
      </tr>
      <tr>
        <th>Trotting</th>
        <th>Left turning</th>
        <th>Walking</th>
      </tr>
      <tr>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/9-trotting.mp4"></source>
          </video>
        </td>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/10-left_turning.mp4"></source>
          </video>
        </td>
        <td>
          <video width="100%" height = "auto" controls>
            <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video_seg/11-walking.mp4"></source>
          </video>
        </td>
        <td> </td>
      </tr>
  </tbody>
</table>

The 15-minute experimental data were decomposed into 936 NM bouts, and embedded these bouts in a low-D space:
- a. Firstly, a 936×936 segment kernel matrix was constructed using the DTAK metric. This segment kernel matrix can flexibly represent the relationship and provide valuable insights between each behavioral component sequence in their feature space.
- b. Because of the high-dimensionality of behavior, we adopted an algorithm called UMAP which can preserve both local and global structure of the dataset. Provide us a 2D embeddings of these NM segments.
- c. The combination of 2D NM space and motion dimension provide a 3D movements space representation.

<video width="100%" height = "auto" controls="controls">
  <source type="video/mp4" src="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video3-cluster_embeddings.mp4"></source>
</video>

Video3 | Spatio-temporal feature space of behavioral components <a href="http://bcbdi.siat.ac.cn/BehaviorAtlas/Video3-cluster_embeddings.mp4" target="_blank">Video3-cluster_embeddings.mp4 (14.6MB)</a> 

---


## About the project



### License

Behavior Atlas is distributed by an [MIT license](https://en.wikipedia.org/wiki/MIT_License).

### Contributing


#### XXX


