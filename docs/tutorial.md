---
layout: default
title: Tutorials
nav_order: 3
---

# Tutorials
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

This tutorial provides the full procedure of Behavior Atlas (BeA) framework. The MATLAB script of BeA was written in section, which could be run in substep. Demo data was attached to Data Resource. Download demo data and open `run.m` of BeA in MATLAB, then you could enjoy BeA by this turorial !

### Add BeA path to MATLAB working path.

``` 
clear all
genPath = genpath('./');
addpath(genPath)
```

### Define the data path

Change your demo data path and name by assigning variables `filepath` and `fileName`.

``` 
%% get filename
filepath = '.\data';
fileName = 'demo_single_Data3d.mat';
```

### Define the video path

Change your demo video path and name by assigning variables `videopath` and `videoName`. This step only need to provide any of the four captured videos for subsequent viewing of the decomposition results.

```
videopath = '.\data';
videoName = 'demo_single_Data3d.avi';
```

### Import dataset
Import the dataset by using the `import_3d` function

```
global BeA
data_3d_name = [filepath,'\',fileName];
import_3d(data_3d_name);
```

### Import video information 

Import video information by using the `import_video` function

```
video_name = [videopath,'\',videoName];
import_video(video_name);
```

### Artifact correction 

Correct the artificials of raw data. We prodive two default method `'median filtering'` and `'adaptive median filtering'`  to simplify the preprocessing. The preprocessing functions that might be used are in the path of `.\preprocess`, which could be flexibly added to `artifact_correction` function.
```
method = 'median filtering';
WinWD = 1000; %ms
artifact_correction(method, WinWD);
```

The raw data and preprocessed data in BeA struct are filtered by above method and are plotted below.  

![Artifact correction ](https://behavioratlas.netlify.app/imgs/ArtificialCorrection.svg "Figure1") 

Figure1 | An example of artifact correction . 

### Body alignment

```
BA.Cen = 1;
BA.VA = 1;
BA.CenIndex = 13;
BA.VAIndex = 14;
BA.SDSize = 25;
BA.SDSDimens = [40,41,42];
body_alignment(BA);
```

The function of `body_alignment` firstly aligns the back points of all the mice skeletons then it aligns the vector from the back point to the tail root point of all the mice skeletons. The alignment results are plotted below.

![Body alignment](https://behavioratlas.netlify.app/imgs/BodyAlign.svg "Figure3") 

Figure2 | An example of body alignment

###  Features Selection

The variable ``selection``  is a 1x48 vector and indicate the selection time series of mice skeletion which are arranged as [X1,Y1,Z1,X2,Y2,Z2,...,Xn,Yn,Zn].

```
body_parts = BeA.DataInfo.Skl;
nBodyParts = length(body_parts);
weight = ones(1, nBodyParts);
featNames = body_parts';
selection = [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,...
            1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,...
            1,1,1,1,0,0,1,1,0,1,0,0,0,0,0,0];
for i = 1:nBodyParts
    BeA_DecParam.FS(i).featNames = body_parts{i};
    BeA_DecParam.FS(i).weight = weight(i);
end
BeA_DecParam.selection = selection;
```
### Behavior Decomposing
This section defines two sets of of parameters corresponding to two layers (poses and movements) decomposition respectively.

``` 
% BeA_SegParam.L1
BeA_DecParam.L1.ralg = 'merge';
BeA_DecParam.L1.redL = 5;
BeA_DecParam.L1.calg = 'density';
BeA_DecParam.L1.kF = 96;

% BeA_SegParam.L2
BeA_DecParam.L2.kerType = 'g';
BeA_DecParam.L2.kerBand = 'nei';
BeA_DecParam.L2.k = 24; % Cluster number
BeA_DecParam.L2.nMi = 100; % Minimum lengths (ms)
BeA_DecParam.L2.nMa = 2000; % Maximum lengths (ms)
BeA_DecParam.L2.Ini = 'p'; % Initialization method
behavior_decomposing(BeA_DecParam);
```

Finally, the function of `behavior_decomposing`  decomposes the continuous time series of mice skeletion in poses and movements segments then clustering them in low demension embedding. The poses embedding (left) and movements embedding (right) are plotted below. More detail analysis could be found in our paper. 

![Embeddings of poses and movements](https://behavioratlas.netlify.app/imgs/pose&mvEmbedding.svg "Figure3") 

Figure3 | Embeddings of poses and movements


