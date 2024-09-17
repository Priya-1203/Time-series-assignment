# Time-series-assignment
Priyavarshini R
127177022
Explanation of the code:

1.Importing Libraries
import numpy as np
import matplotlib.pyplot as plt
numpy is imported as np to handle numerical operations efficiently, such as arrays and mathematical calculations.
matplotlib.pyplot is imported as plt to plot graphs of the data, trend, and seasonality.

2. Moving Average for Odd Length Data
•  moving_average_odd: This function calculates the moving average of data points when the data length is odd.
•  data: Input data array.
•  q: The window size parameter, controlling how many data points before and after the current point should be considered.
•  n = len(data): The total number of data points.
•  m_t = np.zeros(n): Creates an array m_t of zeros with the same length as the input data to store the trend values.
•  Loop (for t in range(q, n - q)): For each element in the data array, starting from q to n-q (to avoid boundary issues), the moving average is calculated over a window of size 2q + 1.
•  m_t[t] = np.mean(data[t-q:t+q+1]): The average of the values in the window centered at t is assigned to m_t[t].
•  return m_t: Returns the trend as a moving average.

3. Moving Average for Even Length Data
•  moving_average_even: This function is for when the number of data points is even.
•  d = 2*q: Here, d represents the total number of elements being averaged, except the boundaries.
•  m_t[t] = (0.5 * data[t-q] + np.sum(data[t-q+1:t+q]) + 0.5 * data[t+q]) / d: The first and last elements of the window have half weight, while the others have full weight. This is divided by d to compute the moving average.
4. Calculating w_k
•  calculate_w_k: This function calculates the seasonality and irregularity combined (denoted by w_k).
•  n = len(data): Get the length of the input data.
•  w_k = np.zeros(n): Initialize w_k as a zero array to store results.
•  Outer loop (for k in range(n)): For each index k, compute seasonality.
•  Inner loop (for j in range(-(n // d), n // d)): This loop accumulates differences between data points and the trend over periods of length d.
•  if 0 <= k + j*d < n: This condition ensures the summation only happens for valid indices.
•  summation += data[k + j*d] - trend[k + j*d]: Calculate the difference between the data and trend values for a given lag.
•  w_k[k] = summation / count: Compute the average of the seasonal component.
•  Return w_k: This array captures the seasonality and irregularity.

5. Calculating g_k (Seasonality)
•	calculate_g_k: This function calculates pure seasonality (g_k) by removing the mean of w_k.
•	avg_w = np.mean(w_k): Compute the average value of the seasonality/irregularity array w_k.
•	g_k = w_k - avg_w: Remove the average component from w_k to isolate the seasonal component.
•	Return g_k: This is the seasonality at each time point.

6. Input Data and Trend Calculation
•	data = np.array([...]): The input time series data.
•	q = 3: The window size parameter for the moving average.
•	if len(data) % 2 == 1: Depending on whether the number of data points is odd or even, the appropriate moving average function is chosen to compute the trend.

7. Calculate w_k and g_k
•  w_k = calculate_w_k(data, trend, q): Compute seasonality and irregularity based on the data and the trend.
•  g_k = calculate_g_k(w_k, q): Isolate the seasonality from the combined seasonality and irregularity.

8. Plotting the Data
•  plt.figure(figsize=(10, 6)): Creates a new figure of size 10x6 inches for the plots.
•  plt.subplot(2, 1, 1): Creates the first subplot in a 2-row layout for the original data and trend.
•	plt.plot(data, ...): Plots the original data.
•	plt.plot(trend, ...): Plots the trend (calculated moving average).
•	plt.title('Original Data and Trend'): Adds the title.
•	plt.legend(): Adds a legend.
•  plt.subplot(2, 1, 2): Creates the second subplot for seasonality.
•	plt.plot(g_k, ...): Plots the calculated seasonality (g_k).
•	plt.title('Seasonality'): Adds the title.
•  plt.tight_layout(): Adjusts the layout so that subplots don't overlap.
•  plt.show(): Displays the plot.

