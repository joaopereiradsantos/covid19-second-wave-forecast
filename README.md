# Forecasting One Week of Portugal's Confirmed COVID-19 Cases
## A Second Wave Analysis Challenge, Hack@Home Vol. III by Tech@Católica

LinkedIn Article: https://bit.ly/3498aOH

On December 5th 2020, Carolina Ferreira, Jerónimo Gama, Pedro Luis Gomes, Rui Pedro Oliveira and myself decided to participate on the Hack@Home Vol. III by Tech@Católica and Católica Lisbon - CTIE.

![alt text](https://github.com/joaopereiradsantos/covid19-second-wave-forecast/blob/main/images/winner.png?raw=true)

**We were challenged to forecast one week of COVID-19 cumulative confirmed cases.** We focused our analysis on Portugal's second wave up until 2020-11-25 and predicted the confirmed cases from 2020-11-25 to 2020-12-02.

From a Logistic Regression to Machine Learning forecasting models like ARIMA and Prophet, we managed to accomplish a final mean absolute percentage error **(MAPE) of 0.7%**.

![alt text](https://github.com/joaopereiradsantos/covid19-second-wave-forecast/blob/main/images/portugal_total_cum_cases.png?raw=true)

While a logistic regression might work well with the total cumulative confirmed cases, it's interesting to dive deep into what are **ARIMA** and **Prophet** models and why they achieved better results:

**ARIMA** stands for autoregressive integrated moving average, while its variant, SARIMAX is similar and adds seasonality and exogenous factors. In an autoregressive (AR) model, the model predicts the next data by analyzing prior data points and applying a mathematical formula similar to linear regression. The integration part (I) takes the difference of the time-series by subtracting the previous value from each new value. Finally, a moving average (MA) model performs calculations based on the noise in the data along with the data’s slope. The purpose of each of these features is to make the model fit the data as well as possible and for that, the pmdarima package and python's auto_arima automatic hyperparameters optimization were of great use. Interestingly, the best ARIMA model parameters only accounted for the Integrated part (or d parameter: number of nonseasonal differences needed for stationarity). [1] [2]

ARIMA models are capable of including seasonal covariates, but adding these covariates leads to extremely long fitting times and requires modeling expertise that many forecasting novices, like ourselves, would not have. That is why Facebook designed the open-sourced **Prophet** model. The model acts as a black-box model but in reality, it allows for a fast forecasting model that has easily interpretable parameters that can be changed by the analyst to impose assumptions on the forecast. Prophet is a decomposable time-series model and accounts for piecewise trends, seasonality, holiday effects and is robust to noise. A model-driven by both the nature of the time series forecasted at Facebook as well as the challenges involved in forecasting at scale. [3] [4]

![alt text](https://github.com/joaopereiradsantos/covid19-second-wave-forecast/blob/main/images/forecast_cum_cases.png?raw=true)

In reality, even if a simpler ARIMA model predicted accurately one week of confirmed cumulative cases, forecasting models applied to a cumulative dataset are not really a correct application of forecasting models. Instead, forecasting models would achieve better results if applied to the variation of daily confirmed cases. Using the same models, a lower mean absolute error (MAE) was achieved for the test dataset. Unfortunately, we settled for a basic primary hyperparameters optimization but we are sure that we could further improve the models' accuracy with a more in-depth parameters analysis while also training the models for other countries' daily confirmed cases.

![alt text](https://github.com/joaopereiradsantos/covid19-second-wave-forecast/blob/main/images/forecast_day_cases.png?raw=true)

Overall, the challenge allowed us to dive deeper into forecasting models while also appreciating how well logistic regressions, exponential, and Gompertz models work with growth analysis. There are clear limitations at predicting longer time intervals and more features would be needed to be taken into account.

XGBoost and Neural Networks algorithms were also considered and can be found on the same .ipynb files at the repository. For a more technical learning, we recommend reading the linked articles and papers regarding the models' application and trying it out yourselves using the same dataset for a similar practical learning experience.

Visualizations inspired by: xkcd using matplotlib.pyplot.xkcd

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install pmdarima.

```bash
!pip install pmdarima
```
## License
[MIT](https://choosealicense.com/licenses/mit/)
