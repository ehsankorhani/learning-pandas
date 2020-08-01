# Filtering

Comparison is the basis for filtering.

If we write a filter like below:

```py
df['make'] == 'Porsche'
```

The result would be a Series:

```bash
0    False
1     True
2    False
Name: make, dtype: bool
```

The trues are the rows that met the criteria.

But we can assign this comparison to a variable in this way:

```py
filt = (df['make'] == 'Porsche') # 'filter' is a reserved word in python and cannot be used
df[filt]
```

We get a DataFrame back:

```bash
	make	model	engin_volume	plate_no
1	Porsche	911	3500	ABC12RR
```

The alternative way is do enter the filter directly in the main DataFrame brackets:

```py
df[df['make'] == 'Porsche']
```

The preferred method is actually to use ```loc``` indexer. ```loc``` can filter rows based on a series of boolean values. Therefore:

```py
df.loc[filt]
```

The advantage to using ```loc``` is that we can specify the columns we want to get in the final result.

```py
df.loc[filt, 'model'] # first parameter are the rows and second one is the columns
```

```bash
1    911
Name: model, dtype: object
```

<br>

## Chain methods

We can use ```&``` and ```|``` operators to chain the filters.

```py
filt = (df['make'] == 'Porsche') & (df['model'] == '911')
df.loc[filt]
```

or

```py
filt = (df['make'] == 'Porsche') | (df['make'] == 'Nissan')
df.loc[filt]
```

Output:

```bash
make	model	engin_volume	plate_no
0	Nissan	Skyline	3000	CMZ10AQ
1	Porsche	911	3500	ABC12RR
```

<br>

## Negate

The ```~``` can be used to negate the result set:

```py
df.loc[~filt]
```

Will output:

```bash
make	model	engin_volume	plate_no
2	BMW	M1	4500	PLF99AZ
```

<br>

## Stack-overflow Survey

Example: get list of all people with salary higher than $70,000.


```py
high_salary = (df['ConvertedComp'] > 70000)
df.loc[high_salary]
```

or 

```py
df.loc[high_salary, ['Country', 'LanguageWorkedWith', 'ConvertedComp']]
```

<br>

## Filter by list

We can input a list of items to filter the DataFrame.

```py
countries = ['United States', 'Australia', 'Canada']
filt = df['Country'].isin(countries)
```

<br>

## String method

We can filter based on string that is inside a column.

```py
filt = df['LanguageWorkedWith'].str.contains('Python', na=False) # na for NaN values
df.loc[filt, 'LanguageWorkedWith']
```