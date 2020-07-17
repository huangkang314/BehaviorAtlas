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

### Define the path of your data

Change your demo data path and name by assigning varibles ``filepath`` and ``fileName``.

``` 
%% get filename
filepath = 'Z:\hanyaning\BehaviorAtlas_version_control\data\three_d';
fileName = 'demo_single_Data3d.mat';
```

### Change your demo video path and name of varibles ``videopath`` and ``videoName``.

```
%% get videoname
videopath = 'Z:\hanyaning\BehaviorAtlas_version_control\data\videos';
videoName = 'demo_single_Data3d.avi';
```

### Import dataset from varibles ``filepath`` and ``fileName``.

```MATLAB
%% Import dataset
clear global
global BeA
data_3d_name = [filepath,'\',fileName];
import_3d(data_3d_name);
```

### Import video information from varibles ``videopath`` and ``videoName``.

```MATLAB
%% Import dataset
video_name = [videopath,'\',videoName];
import_video(video_name);
```

### Artifact correction of raw data. We prodive two default method ``'median filtering'`` and ``'adaptive median filtering'``  to simplify the preprocessing. The preprocessing functions that might be used are in the path of ``.\preprocess``, which could be flexibly added to ``artifact_correction`` function.
```MATLAB
%% Preprocess ->  Artifact Correction
method = 'median filtering';
WinWD = 1000; %ms
artifact_correction(method, WinWD);
```

The raw data and preprocessed data in BeA struct are filtered by above method and are plotted below.  
![0d899c3075bcd8e632cdf21b637868a0.svg+xml](en-resource://database/521:0)

#### 7. Body alignment. 

```MATLAB
%% Aanlysis  -> 1. body alignment
BA.Cen = 1;
BA.VA = 1;
BA.CenIndex = 13;
BA.VAIndex = 14;
BA.SDSize = 25;
BA.SDSDimens = [40,41,42];
body_alignment(BA);
```

The function of ``body_alignment`` firstly aligns the back points of all the mice skeletons then it aligns the vector from the back point to the tail root point of all the mice skeletons. The alignment results are plotted below.
![62cb508935249c88a338760f409c48e2.svg+xml](en-resource://database/527:0)

###  Select the features for analysis. The variable ``selection``  is a 1x48 vector and indicate the selection time series of mice skeletion which are arranged as [X1,Y1,Z1,X2,Y2,Z2,...,Xn,Yn,Zn].

```MATLAB
%% Aanlysis -> 2. Feature Selection
body_parts = BeA.DataInfo.Skl;
nBodyParts = length(body_parts);
weight = ones(1, nBodyParts);
featNames = body_parts';
selection = [1,1,1,1,1,1,1,1,...
            1,1,1,1,1,1,1,1,...
            1,1,1,1,1,1,1,1,...
            1,1,1,1,1,1,1,1,...
            1,1,1,1,0,0,1,1,...
            0,1,0,0,0,0,0,0];
for i = 1:nBodyParts
    BeA_DecParam.FS(i).featNames = body_parts{i};
    BeA_DecParam.FS(i).weight = weight(i);
end
BeA_DecParam.selection = selection;
```
### Behavior Decomposing. 

``` MATLAB
%% Aanlysis -> Behavior Decomposing
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

Finally, the function of ``behavior_decomposing``  cuts the continuous time series of mice skeletion in poses and movements segments then clustering them in low demension embedding. The poses embedding (left) and movements embedding (right) are plotted below. More detail analysis could be found in our paper. 
![8323869fd6d085182d50ecfeb742f15f.svg+xml](en-resource://database/533:0)


