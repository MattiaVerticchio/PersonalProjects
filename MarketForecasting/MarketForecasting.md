# Market Forecasting
> **Italiano** / [English](https://github.com/MattiaVerticchio/PersonalProjects/blob/master/MarketForecasting/MarketForecasting_EN.md)
>
> _Nota: Questo repository non contiene il dataset di training e l'implementazione del benchmark a causa di dubbi sulla licenza utilizzata._

> **Sommario**
>
> Questo progetto è incentrato sulla previsione di indici di mercato a partire da serie storiche, su un orizzonte temporale di 65 giorni. Il dataset contiene 19 colonne che comprendono tre diverse classi di asset: azioni, obbligazioni e liquidità. L’intervallo temporale coperto è il periodo 2015-2019. Il framework utilizzato è sviluppato da H2O.ai, ed eseguito su Google Colab. I risultati sono confrontati con la _Gated Recurrent Neural Network_ sviluppata da Armundia Group e ottenuta durante la frequentazione del corso universitario in Machine Learning. I nuovi risultati superano significativamente il benchmark, in particolare vi è una riduzione del ~90% dell'errore di previsione per i rendimenti non cumulativi e del ~27% per quelli cumulativi, con alcuni indici che hanno prestazioni migliori di altri.


## Introduzione
L'obiettivo di questo progetto è la previsione dell’andamento di indici di mercato. Il dataset è composto da 19 indici e copre un periodo di 4-5 anni.
Il modello sarà testato sugli ultimi 65 giorni.
La metrica di riferimento è la riduzione percentuale dell'errore assoluto medio (MAE) per ciascun asset, che è definito come segue:

<p align = "center">
<img src = "https://latex.codecogs.com/svg.latex?\text {MAE} = \ frac {1} {n} \ sum_ {i = 1} ^ {n} | Y_i-y_i |" />
</p>

_Y_ è il valore reale del set di test, _y_ è la previsione del modello e _n_ è 65, l'orizzonte di previsione.

Ho addestrato un modello di aumento del gradiente per ogni indice, invece di un GRNN comune per tutti gli indici, e ho ottimizzato la pipeline attraverso l'evoluzione genetica con H2O.ai Driverless AI.

I modelli che aumentano il gradiente sono studenti di ensemble. Usano gruppi di alberi decisionali per superare i semplici regressori presi singolarmente.

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
