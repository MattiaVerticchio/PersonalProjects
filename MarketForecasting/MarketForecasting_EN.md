# Market Forecasting
> [Italiano]() / **English**
>
> _Note: This repository doesn’t contain the training dataset and the benchmark implementation due to licensing concerns._

> **Abstract**
>
> This project focuses on forecasting market indices from time-series, over a 65 days horizon. The dataset contains 19 columns comprising three different asset classes: equity, bond, and liquidity. It covers the 2015–2019 frame. The framework is H2O.ai software, executed on Google Colab. The results are compared to Armundia Group’s GRU neural network obtained during the university course in Machine Learning. The new results significantly outperform the benchmark, in particular there are a ~90% reduction in forecasting error for non cumulative yields, and ~27% reduction for cumulative ones, with some indices performing better than others.

## Introduction
The objective of this project is the prediction of future market indices. The dataset covers 19 indices and 4–5 years.
We’ll test the model on the last 65 days.
The improvement metric is the percent reduction in mean absolute error (MAE) for each asset, which is defined as follows:

<p align="center">
<img src="https://latex.codecogs.com/svg.latex?\text{MAE}=\frac{1}{n}\sum_{i=1}^{n}|Y_i-y_i|"/>
</p>

_Y_ is the actual value of the test set, _y_ is the model’s forecast, and _n_ is 65, the forecasting horizon. 

I trained a gradient boosting model for each index, instead of a common GRNN for all the indexes, and optimized the pipeline through genetic evolution with H2O.ai Driverless AI.

Gradient boosting models are ensemble learners. They use groups of decision trees to outperform the simple regressors taken singularly.

## Results
As stated before, the benchmark is a GRNN model. I’m comparing the results of the new models against the predictions that came with the original project dataset and notebook.
Gradient boosting models brought an average ~27% reduction in mean absolute error in post cumulative yields and a ~90% reduction in pre cumulative ones.

### Improvement
The following table represents the detailed results of the % reduction in MAE.
A higher % means better accuracy, while negative values mean worse predictions.

| Index | Pre | Post |
| ----- | -----| ----- |
| MXEM | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 95.2 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 72.0 % |
| MXEU | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 93.6 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 68.1 % |
| MXNA | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 77.8 % | <img src="https://via.placeholder.com/12/f03c15/000000?text=+"/> -38.4 % |
| MXEF | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 94.6 % | <img src="https://via.placeholder.com/12/f03c15/000000?text=+"/> -76.0 % |
| MXJP | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 90.5 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 57.2 %|
| MXPC | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 94.0 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 61.2 % |
| JPMGEMLC | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 83.6 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 35.5 % |
| JNUCUK | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 76.9 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 75.8 % |
| SBF14T | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 90.1 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 59.0 % |
| ER00 | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 92.6 % | <img src="https://via.placeholder.com/12/f03c15/000000?text=+"/> -48.9 % |
| UC00 | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 85.9 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 23.3 % |
| JNUCUS | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 96.0 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 61.4 % |
| C0A0 | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 94.0 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 63.7 % |
| JPEGCOMP | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 95.1 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 61.7 % |
| JNUCJP | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 76.7 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 20.4 % |
| JC00 | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 70.7 % | <img src="https://via.placeholder.com/12/f03c15/000000?text=+"/> -69.4 % |
| JPCAEU3M | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 99.6 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 9.8 % |
| JPCAGB3M | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 99.3 % | <img src="https://via.placeholder.com/12/f03c15/000000?text=+"/> -13.9 % |
| JPCAUS3M | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 99.9 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 89.1 % |
| Average | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 89.8 % | <img src="https://via.placeholder.com/12/29cc90/000000?text=+"/> 26.9 % |

### Plots

<p align="center">
  <img width="400" src="preplots/MXEM.svg">
  <img width="400" src="postplots/MXEM.svg">
</p>


<p align="center">
  <img width="400" src="preplots/MXEU.svg">
  <img width="400" src="postplots/MXEU.svg">
</p>


<p align="center">
  <img width="400" src="preplots/MXNA.svg">
  <img width="400" src="postplots/MXNA.svg">
</p>


<p align="center">
  <img width="400" src="preplots/MXEF.svg">
  <img width="400" src="postplots/MXEF.svg">
</p>


<p align="center">
  <img width="400" src="preplots/MXJP.svg">
  <img width="400" src="postplots/MXJP.svg">
</p>  


<p align="center">
  <img width="400" src="preplots/JPMGEMLC.svg">
  <img width="400" src="postplots/JPMGEMLC.svg">
</p>


<p align="center">
  <img width="400" src="preplots/JNUCUK.svg">
  <img width="400" src="postplots/JNUCUK.svg">
</p>


<p align="center">
  <img width="400" src="preplots/SBF14T.svg">
  <img width="400" src="postplots/SBF14T.svg">
</p>


<p align="center">
  <img width="400" src="preplots/ER00.svg">
  <img width="400" src="postplots/ER00.svg">
</p>


<p align="center">
  <img width="400" src="preplots/UC00.svg">
  <img width="400" src="postplots/UC00.svg">
</p>


<p align="center">
  <img width="400" src="preplots/JNUCUS.svg">
  <img width="400" src="postplots/JNUCUS.svg">
</p>


<p align="center">
  <img width="400" src="preplots/C0A0.svg">
  <img width="400" src="postplots/C0A0.svg">
</p>


<p align="center">
  <img width="400" src="preplots/JPEGCOMP.svg">
  <img width="400" src="postplots/JPEGCOMP.svg">
</p>


<p align="center">
  <img width="400" src="preplots/JNUCJP.svg">
  <img width="400" src="postplots/JNUCJP.svg">
</p>


<p align="center">
  <img width="400" src="preplots/JC00.svg">
  <img width="400" src="postplots/JC00.svg">
</p>


<p align="center">
  <img width="400" src="preplots/JPCAEU3M.svg">
  <img width="400" src="postplots/JPCAEU3M.svg">
</p>


<p align="center">
  <img width="400" src="preplots/JPCAGB3M.svg">
  <img width="400" src="postplots/JPCAGB3M.svg">
</p>


<p align="center">
  <img width="400" src="preplots/JPCAUS3M.svg">
  <img width="400" src="postplots/JPCAUS3M.svg">
</p>

## Conclusions
The new models have overall better scores than the GRU neural network. Of course, they aren’t perfect.
In some isolated indices, the new models didn’t outperform the benchmark, requiring further tuning and engineering.
Gradient boosting models, however, brought a stable overall reduction in forecasting error in the pre cumulative yields (90%).

In conclusion, what could we furtherly improve?

1. Adjusting the training data for inflation over the observations time-frame.
1. Updating the dataset extending the period covered by observations. Some indexes (E. G. MSCI ones) cover decades, while the available dataset covers ~5 years only.
1. Increasing sampling frequency, adding intraday asset data.
1. Disaggregate the index compositions.
1. Introduce more assets or exogenous features that can impact the prediction, like macroeconomic indicators, notable events, and local holidays.
1. Augment the dataset using signal processing metrics: moving average, exponential smoothing, LOESS regression, cross-covariance, cross-correlation, feature interaction.
1. Introduce a natural language processing component based on news streams and financial docs, like SEC filings and analysts’ predictions.


Finally, we could take a look at the research side.
As of today, the state-of-the-art for multi-variate time series forecasting seems to be [GRU-ODE-Bayes](https://arxiv.org/abs/1905.12374), [Latent ODEs](https://arxiv.org/abs/1907.03907v1) and [LSTM](https://arxiv.org/abs/1612.02130v2) networks.



[**Go back to index >**](https://github.com/MattiaVerticchio/PersonalProjects/blob/master/README_EN.md)
