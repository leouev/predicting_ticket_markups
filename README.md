Analyzing Concert Data to Predict Ticket Price Markups

Author: Evan Paul
https://www.linkedin.com/in/evan-paul-b4b94a55 

GitHub link: https://github.com/epsilon670/predicting_ticket_markups 
Overview
This was my final project for General Assembly’s part time Data Science class given in San Francisco from January-April 2016 (https://generalassemb.ly/education/data-science).

The goal was to build a model that could predict the ticket markup of a concert on StubHub.com (an online ticket re-selling marketplace) given inputs about the concert. If these values could be predicted, a ticket re-seller could use the prediction to estimate an ideal selling price when posting their tickets on StubHub. Similarly, a concertgoer could use the predictions to estimate how much they would need to pay in order to buy tickets for a given show from StubHub.

A slideshow deck outlining this project, its scope, and my key findings can be viewed in the Analyzing Concert Data to Predict Ticket Price Markups.pdf file.
Data Collection
I collected the data for this project from 3 primary sources:

StubHub’s Web API (to get StubHub ticket price data for concerts)
Web scrapes of SongKick.com (to get ticket face values and “sold out” statuses for concerts)
EchoNest Web API (to get data relating to concert artists’ popularities)

I collected this data for concerts in 16 metropolitan areas across the United States. To ensure consistency between concerts, I collected all data on March 13th, 2016. The code for collecting all data for each metro area can be viewed in the Initial_Data_collection.ipynb notebook and the code for aggregating all of the metro area concert data together can be viewed in the Create_master_dataframe.ipynb Jupyter notebook.

In total, I collected data for 3,126 concerts. This raw, unprocessed data can be found in the Data/MasterTicketData.csv file.

Data Processing and Cleaning
Once the data was collected, I ran Python code to process the data and clean it. This included:

Removing concerts with non-numeric ticket prices
Calculating ticket markup by subtracting face value from StubHub’s minimum ticket price
Removing outliers (using the IQR method)
Converting variables with large skews to logarithmic form

The code for the processing and cleaning can be found in the Process TicketData.ipynb notebook. The code for converting feature values into logarithmic form can be viewed in the Examine Variable Distributions & Skews.ipynb notebook.

The final processed data set of 1,192 concerts is in the Data/ProcessedTicketDataLogs.csv file.

Noteworthy problem with data - the web scrapes of SongKick did not always yield the correct “sold out” values. Only 80 out of 1,192 concerts are listed as “sold out” in the data. I’ve confirmed that at least 1 show (and likely many more) marked as “not sold out” in the dataset was actually sold out in reality. Therefore, it is highly likely that the dataset underrepresents the true number of sold out shows (meaning that the impact of a show being sold out is underestimated in the resulting models).
Regression Model
Once a clean and processed dataset was created, I then used the RandomForestRegressor package from sklearn.ensemble to build a Random Forest model for ticket markup prediction. The code for this can be viewed in the Ticket Markup Prediction Model.ipynb notebook.
Classification Model
In order to try and get more accuracy in the predictions, I then tried to build a classification model to predict the dollar range that a concert ticket’s markup would be in. This followed the same process as in regression, except I used RandomForestClassifier from sklearn.ensemble in order  to classify each concert into one of the following buckets:

Bucket 1: Ticket markup between $0 - $25 
Bucket 2: $25 - $37
Bucket 3: $37-$52
Bucket 4: >$52
The code for the classification model can be viewed in the Ticket Markup Classification Model.ipynb notebook.
Linear Regression
I also used Lasso and Linear Regression on the data in order to see whether there were any interesting insights that could be gleaned from the dataset. The code for this can be found in the Linear Regression for Stubhub Markup.ipynb notebook. See the Analyzing Concert Data to Predict Ticket Price Markups.pdf file for the results.
Libraries and 3rd Party Packages
I used the following libraries in this project:

Pandas
sklearn
NumPy
Matplotlib
statsmodels.formula.api
Beautiful Soup (for web scraping)

Suggestions, feedback, comments, and pull requests are all welcome.
