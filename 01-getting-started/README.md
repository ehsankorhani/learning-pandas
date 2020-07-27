# Getting Started

Import ```pandas``` In the new Python3 Notebook.

```py
import pandas as pd # pd is a common convention
```
(shift + enter)

Because our data is in CSV format:

```py
df = pd.read_csv('data/survey_results_public.csv') # df = data frame
```

Data Frame is rows and columns of data.

To view the data frame:

```py
df
```

Jupyter by default will display only 20 columns of data.

There are few methods to find out more about the real data in the data frame.

### shape

Will give us the real number of rows and columns:

```py
df.shape # (64461, 61)
```

### info

This method will give us more information, such as data type of the columns.

```py
df.info()
```

and the output will be:

```
#   Column                        Non-Null Count  Dtype  
---  ------                        --------------  -----  
 0   Respondent                    64461 non-null  int64  
 1   MainBranch                    64162 non-null  object 
 2   Hobbyist                      64416 non-null  object
 3   Age                           45446 non-null  float64
 4   Age1stCode                    57900 non-null  object 
 5   CompFreq                      40069 non-null  object 
 ...
```

### set_option

Now that we now about the size of the data frame we can set an option to view all the columns or rows.

```py
pd.set_option('display.max_columns', 61)
pd.set_option('display.max_rows', 61)
df
```

### head

If you don't want to see all the records ```head()``` function can be used to only display first five rows:

```py
df.head()
```

Or pass it a parameter for how many records we would like to see:

```py
df.head(10)
```

### tail

Same as ```head()``` but will display the last records.

```py
df.tail(10)
```

<br>

## Read schema
In a same way we can create a data frame to read the schema file.

```py
schema_df = pd.read_csv('data/survey_results_schema.csv')
schema_df
```

And the output will be:

```
	Column	QuestionText
0	Respondent	Randomized respondent ID number (not in order ...
1	MainBranch	Which of the following options best describes ...
2	Hobbyist	Do you code as a hobby?
...
```

This schema will help us understand the main data frame.

