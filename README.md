# Recommender System 2021 Challenge

This repository contains the code used for the [Recommender System 2021 Challenge](https://www.kaggle.com/c/recommender-system-2021-challenge-polimi) hosted by the Recommender Systems course at Politecnico di Milano.
The repository is split in 2 main folders:
* [CustomModels](https://github.com/LacavaMarco/RecSys2021_Govigli_Lacava/tree/main/CUSTOM_MODELS) which contains our custom models and scripts created for the competition
* [GithubModules](https://github.com/LacavaMarco/RecSys2021_Govigli_Lacava/tree/main/GITHUB_MODULES) which contains the [course framework repo](https://github.com/MaurizioFD/RecSys_Course_AT_PoliMi) given by the professor

## Overview

The complete description of the problem can be found in the [kaggle competition page](https://www.kaggle.com/c/recommender-system-2021-challenge-polimi/overview). 

Briefly, given the **User Rating Matrix** and some **Item Content Matrices**, the objective of the competition was to create a recommender for **TV series/Movies**.

The evaluation metric used was the **MAP@10**.

After a preprocessing phase, we used the following dataset:

* **URM**, 
  * **13650** users
  * **18059** items
  * **2.14%** data sparsity
* **ICM**
  * **18059** items 
  * **335** attributes
  * **1.29%** data sparsity

## Strategy
We approached the problem through different stages:
* At first, we performed some **data exploration**, in order to find interesting patterns in the dataset, 
we discovered in fact the following singularities:
  * Some episodes belong to more than one TV series/Movie
  * Some TV series/Movie even if without channel have been seen by some users
  * Some TV series/Movie even if without episodes have been seen by some users
* Then we **profiled** the base models to find the best performers: **SLIM Elastic-Net** outperformed all the other base algorithms with a gap of at least 10%
* The next phase was focused on building **hybrids**, mainly composed by **2 models** at time in order to better control their optimization.

## Best Model

The **ICMs** were not so effective in our experiments, thus we decided to focus on the information contained in the **URM**.
Our best model was in fact a **hybrid between SLIM and iALS**, to improve it we tried the following solutions:
* Hybrids composed by **more than 2 models**
* A **hierarchical structure**: we tried to combine the base models toghether by building a hybrid and iteratively combine it with other base models starting from the algorithms with the lowest MAP
* **Co-trained hybrid models** (composed by 2 models) and their combinations.

The first two improvement solutions gave worst results than SLIM+iALS, while some co-trained hybrids performed better than SLIM+iALS in the validation set but didn't improve the leaderboard score. Since the implementation of the co-trained hybrid models was done in the last days of the challenge, investing more time on them would have probably let us find a new best model.

### Evaluation
- **Public** Leaderboard score: **0.48065**
- **Private** Leaderboard score: **0.48080**

## Group Members
- [__Marco Lacava__](https://github.com/LacavaMarco)
- [__Francesco Govigli__](https://github.com/FrancescoGovigli)
