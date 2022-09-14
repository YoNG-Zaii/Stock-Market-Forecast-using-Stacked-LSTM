# Stock Market Forecast using Stacked LSTM

As stock market prices are time-series data, we can use Recurrent Neural Networks to forecast the future prices. In particular, we will use multiple layers of Long-Short Term Memory (LSTM) to train this model.

### Data Collection

The stock market data is obtained via Tiingo API.

Source: https://api.tiingo.com/documentation/general/overview

We choose closing prices to represent the final stock price of each day.

### Data Normalisation

As the range of the data is quite large and 50% of the data is below 172.97, we need to transform the data to minimise the noise within the data.

Since we have a fixed min and max, we will apply MinMax scaler provided by scikit-learn. As a result, our transformed data will be in the range [0, 1].

Scaling also helps the model to converge faster during training.

### Model Training

We use three layers of LSTMs and one layer of fully-connected layer. We also apply sigmoid activation function in the first layer of LSTM and the fully-connected layer.

Sigmoid activation function is chosen as it ensures the output to be in the range [0, 1]. During prediction, this output can be transformed back to its original values.

We use previous 100-day input to predict the next-day closing price. For example, to predict the 101th day's price, we use 1st, 2nd, 3rd, ..., and 100th values altogether.

### Model Prediction

As a performance metric, we will evaluate the root mean squared error between the actual values and the predicted values to determine how well the model performs.

#### Forecasting

We use the trained model to predict closing prices of 30 days in the future.

### Extra

For this section, we remove the last 30-day closing prices so that another model can be trained without the last 30 days. Then, the model is used to predict the missing last 30-day values.
