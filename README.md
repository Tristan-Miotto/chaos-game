# The chaos game

This is a personal project developed in 2024.

## Description of the project

Originally, the chaos game referred to a method of creating a **fractal**, using a polygon and an initial point selected at random inside it. The fractal is obtained by iteratively creating a sequence of points, starting with the initial random point, in which each point in the sequence is a given fraction of the distance between the previous point and a random vertex of the polygon. Moreover, we can define some specific constraints inside the iterations. For example, we can implement the fact that it is not possible to select a vertex twice in a row. Then, we get a totally different fractal. 

In this repository, I implement the chaos game in **Python** so that we can try with different...
- Numbers of vertices $n$ of the polygon.
- Number of iterations *n_iter*. The higher *n_iter* is, the better we can see the fractal. 
- Steps (the fraction of the distance between the previous point and the current one).
- Constraints.

The concept of chaos game is more general than that. We can obtain many different fractals with various shapes. For instance, it is possible to get a fern (called **Barnsley fern**). I implemented it. 
I also made an animation with FFMpegWriter from matplotlib.animation. Then, we can observe each point appearing one by one and the fern emerging.

Finally, with FFMpegWriter and CapCut (an editing software), I made a video that shows how the chaos game works. 

## Content of the repository

This repo contains:

### 1 – A *data_processing.ipynb* Jupyter Notebook 💻

Before running this code, we need to download the [Audio MNIST](https://www.kaggle.com/datasets/sripaadsrinivasan/audio-mnist) dataset available in Kaggle. The program provided transforms each audio signal to a **mel spectrogram**. They represent sounds with a frequency scale that more closely resembles how humans perceive pitch. Mel spectrograms will constitute the input data of our model. Finally, the program save the data (train and test) as well as normalization data (min and max) in a *data* folder.

### 2 – A *generation.ipynb* Jupyter Notebook 💻

In this Python file, we build a variational autoencoder (VAE) that generates virtual voices.
- First, we load data from the *data* folder.
- Then, we create our VAE and we train it with input data (mel spectrograms). As we want our latent space to follow a normal distribution, we need to define the **Kullback-Leibler (KL) divergence**.
- After the training phase of the model, we generate a vector following a standard normal distribution.
- Finally, we denormalize the generated mel spectrogram and we transform it into an audio signal, which we can then listen to.

As a result, we get a virtual voice (it looks like a robot) saying a digit. Most of the time, we can recognize the number pronounced. We assume that, to obtain clearer sounds, we need to improve the quality of the mel spectrograms. In other terms, we must increase their dimension (width and height).

### 3 –  A *mathematical_proof_KL_divergence.png* file ➗✖️

KL divergence is a measure that quantifies how one probability distribution $P$ differs from a second $Q$. It is defined as followed :

$$D_{KL}(P \|\| Q) = \int_{-\infty}^{\infty} p(x) \log\left(\frac{q(x)}{p(x)}\right) dx$$

where $p$ (resp. $q$) is the density associated with $P$ (resp. $Q$).

The *mathematical_proof_KL_divergence.png* file contains the written demonstration of the KL divergence in context of VAEs, which is :

$$\frac{1}{2} \sum_{i=1}^{d} \mu_i^2 + \sigma_i^2 - 1 - \log(\sigma_i^2)$$

where $\mu_i^2$ and $\sigma_i^2$ are outputs of the encoder used to build the latent space.

### 4 –  A *report_project_in_french.pdf* file 📄

This document is the report of the project, written is French. It describes more in detail...
- Sound processing.
- The classifaction models that we built.
- The sound generator. In fact, we actually made a **grid search** to find the best combination of hyperparameters. We also experimented with different data preprocessing techniques (dimension of melspectrograms, normalization). Here, to keep it simple, I manually defined the hyperparameters without performing a grid search.

## 📌 Note

⚠️ It seems that the *generation.ipynb* Notebook can't run with a recent version of Tensorflow. However, it's working with the 2.10 version. 

