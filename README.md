# The Bank of Russia's Key Rate Parser

# Project Description
The app's main goal is to parse the most frequent key rate per month in a convinient DataFrame structure. 

Bank of Russia provides SOAP 1.1-API interface, so the "zeep" library was an ideal choice to parse data. The data gets processed and cached into Panda's DataFrame.

# Project Structure

## Variables
"**fromDate, ToDate** YYYY-MM-DD" - Two main variables needed to set the desired date range. ToDate variable must accept the last day of the month since it also be used in `ToDate`s POST XML parameter, which is inclusive.

"**dates**" - Creates a range of dates. *freq* parameter sets the frequency. The default "MS" alias defines month start frequency.

"**df_sales**" - Holds the revenue data to showcase a simple use case.

"**sales_rates_2024**" - Contains parsed rates and dummy revenue values.

## Functions
`get_cbr_key_rate(fromDate:str, ToDate:str) -> pd.DataFrame`
The function parses key rates and caches obtained data with SQLite. The data gets passed into the DataFrame through `read_xml` method where an unnecessary hours part gets truncated.

`df.groupby(df.index.to_period('M')).agg(lambda x: x.mode().iloc[0])` - given some month, this line filters the most frequently met key rate and stores it for that month.

`key_rate_and_sales(func:"a function to get the key rates") -> pd.DataFrame`
Unites the key rates from previous function with the given sales from `df_sales`.

## Graphs
There are two graphs to visualize the data. First bar-graph depicts the revenue and key side by side and the second graph are two splitted line graphs that depicts revenue and key rates on their own.

# Simple Use Case
The parsed data is used for statistical hypothesis testing to check if there are any relations between company's revenue and the key rate.

# Technical Notes
Python 3.13.3. `zeep`, `pandas`, and `matplotlib` as the main modules. `requirements.txt` holds all the necessary dependencies.

The code was written within Jupyter Notebook on **Windows 11** Home, version 24H2, 26100.4061 OS build.

# License
[MIT](https://choosealicense.com/licenses/mit/)
