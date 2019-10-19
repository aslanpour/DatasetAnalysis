# Milano Weather Station‎ Data Analysis
Statistical Analysis for Milano Weather Station Data

Written by:

Mohammad Sadegh Aslanpour

Summary: In this study, the weather condition recorded in Milan city by sensors located within the city limit is statistically analyzed. The collected datasets  provides information about meteorological phenomena intensity and type, where the recorded information includes: wind direction, wind speed, temperature, relative humidity, etc. Among them, we selected the last two parameters to perform statistical analysis as—1) descriptive statistics to identify the distribution of each parameter, 2) inferential statistics to identify the type and strength of relationship between them, 3) regression to represent a formula for their relationship, and 4) machine learning to overcome regression limitations. The analysis is carried out in Java language, and the codes are available in GitHub . Our results shows that while the two parameters: temperature and relative humidity have distinguished distribution pattern, our proposed artificial neural network is perfectly capturing the relationship. The process of this analysis is elaborated in the following paragraphs.

To begin with, the datasets, with 1462 records, contain data recorded by sensors located in via Lambrate Street in Milan from 2013/11/01 to 2013/12/31 on an hour basis for both temperature and relative humidity in Celsius degree and percentage, respectively. The datasets first require to be preprocessed because not only do need the date and time be separated, but also they need to be sorted chronologically. The date and time field in datasets is like “11/28/2013 1:00” for the temperature records while is like “2013/11/28 1:00” for the relative humidity, which we divided them into: year, month, day, and hour (codes in DatasetPreProcessing class). Having done, we created two CSV files for preprocessed the datasets. 
 	 
We then performed descriptive statistics analysis (codes in DescriptiveStatistics class) to evaluate the distribution of the recorded data for temperature and relative humidity. Noticeable point is that, for temperature, the mean (=6.54), median (=6.8), and mode (=7) are in a narrow range reflecting a relatively normal distribution, while the opposite is true in case of relative humidity with 80.31, 88 and 94, respectively. The skewness value can prove this at 0.22 for temperature, i.e. approximately a symmetric distribution. However, the skewness value for relative humidity is –1.66 which means its distribution is negatively-skewed, i.e. long-tailed towards the left. Another important measure here is Kurtosis representing the shape, or particularly the degree of peakedness, of distributions. Kurtosis value for temperature is –0.71 which means the distribution is rather light-tailed with less extreme outliers and a tendency to be normal, whereas for relative humidity is 2.22, indicating a heavy-tailed distribution with many outliers. Hence, the temperature distribution follows a normal-like pattern, but relative humidity an unsymmetrical-like.

 	 

After analyzing our target parameters independently, we have to identify their relationship using inferential statistics, particularly through covariance and correlation measures. We consider temperature as independent and relative humidity as dependent parameters (the opposite would be the case as well) to find the dependency. Our covariance analysis result, i.e. –27.38, shows that the relationship is inverse, meaning that increase in on parameter results in the opposite change in another. The strength and direction of this relationship can be easily interpreted by the correlation (we calculated Pearson correlation). Correlation attempts to draw a line of best fit through the data of two variables. Correlation converts the covariance to a standardized scale of −1 to +1, too. The value for correlation here was –0.33 which indicates that one parameter moves less positively or negatively in relation to changes in another parameter. In other words the two variables do not exhibit a rhythmic movement relative to each other. This might be because there is a weak linear relationship between temperature and relative humidity. Precisely, the data should be normally distributed, while the relative humidity is seemingly not. The analysis codes written for inferential statistics are in InferentialStatistics class.
Either way, to find the actual relationship, between temperature and relative humidity, and to represent a formula, we continue our investigation by making use of regression methods. Linear regression calculates an equation that minimizes the distance between the fitted line and all of the data points. We formulated the linear relationship as y= -1.12x+87.63 where –1.12 is the slope and 87.63 is the y-intercept. Main concern here is that “Does this formula explain the relationship perfectly?”. The answer is to evaluate R2 value which found to be 0.11, meaning that the observations are rather far from the best fit line, and that the strength of the relationship between our formula and parameters is not great. The larger the R2, the better the regression model fits the observations. Codes for this analysis are in Regression class. Hence, the line generated by Simple Regression is not a got representation of the data and a more effective solution is required.
 
Since Simple Regression failed to carefully represent the relationship, we investigated more complex solutions: artificial neural networks (ANN). Of course, in continuous of this study, ARMA, ARIMA and SARIMA could have been the case, but we aimed at bringing the date and time parameters of each record into play, assisting the predictor. To this end, after normalizing the datasets, we divided them into two part: 80% for training the neural network and 20% for testing the accuracy of its predictions of relative humidity based on the observed temperature. The neural network inputs include: month, day, hour, temperature while the output will be a prediction of relative humidity. We examined a wide range of configurations: hidden layer neurons [2-10], learning rate [0.1-0.6], and maximum iterate [100-2000], i.e. 1080 networks, to find the most accurate (All ANN files are in “src/files/nn” folder). To improve the networks, we substituted linear transfer function in output layer with Sigmoid as well. Assessing the performance of ANNs, we came to the configuration with: 6 neuron in RBF (hidden) layer, learning rate of 0.5, and maximum iteration of 200. This ANN is able to perfectly predict the relative humidity with MAE = 4.65, RMSE = 7.94, MAPE = 6%, and PRED (25) = 96% (codes are in MachineLearning class). However, while effective, this solution is still dealing with challenges when significant change in the data is seen, thereby demanding new paradigms of ANNs: deep learning to address, probably. 
 
