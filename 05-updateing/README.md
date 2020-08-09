# Updating Rows and Columns

In this lesson we explore altering data in a DataFrame.

### Changing Columns title

with this command we get the list of column names:

```py
df.columns
# Index(['make', 'model', 'engin_volume'], dtype='object')
```

There are couple of ways to modify the titles:

```py
df.columns = ['brand', 'type', 'engin_volume']
df.columns
# Index(['brand', 'type', 'engin_volume'], dtype='object')
```

In the method above we have to pass all columns names.

But most of times we only want to change only a few columns or we want to alter all titles in a certain way (i.e. capitalize, remove space, etc.).

For this we use ```list comprehension```.

```py
df.columns = [x.upper() for x in df.columns]
# Index(['BRAND', 'TYPE', 'ENGIN_VOLUME'], dtype='object')
```

or 

```py
df.columns = df.columns.str.replace('_', '-')
# Index(['BRAND', 'TYPE', 'ENGIN-VOLUME'], dtype='object')
```

#### Rename

To change only certain columns:

```py
df.rename(columns = {'BRAND': 'make', 'TYPE': 'model'}, inplace = True)
# Index(['make', 'model', 'ENGIN-VOLUME'], dtype='object')
```

<br>

### Changing Rows title

We can get a *row* data with:

```py
df.loc[2]
# make             BMW
# model             M1
# ENGIN-VOLUME    4500
# Name: 2, dtype: object
```

So, it's possible to alter these data with:

```py
df.loc[2] = ['Ford', 'Focus', '1200']
```

To only change few columns:

```py
df.loc[2, ['model']]  = ['Ranger']
# make              Ford
# model           Ranger
# ENGIN-VOLUME      1200
# Name: 2, dtype: object
```

Alternatively:

```py
df.at[2, ['model']]  = ['Ranger']
```

#### Using Filter

```py
filt = (df['make'] == 'Ford')
df.loc[filt, 'ENGIN-VOLUME'] = '5000'
```

### Changing multiple Rows

```py
df['make'] = df['make'].str.lower()
```

<br>

## Advance update methods

There are 4 different methods and they are confusing because they do a very similar job.

* apply
* map
* applymap
* replace

### apply
Is use for calling a function on values. It can work on both ```DataFrame``` and ```Series``` objects.

As an example we can get the length of a field:

```py
df['make'].apply(len)
```

```
0    6
1    7
2    4
Name: make, dtype: int64
```

Apply can call the custom functions as well:

```py
def to_upper(field):
    return field.upper()

df['make'].apply(to_upper)
```
```
0     NISSAN
1    PORSCHE
2       FORD
Name: make, dtype: object
```

We can use this to update data.

```py
df['make'] = df['make'].apply(to_upper)
```
```
	make	model	ENGIN-VOLUME
0	NISSAN	Skyline	3000
1	PORSCHE	911	3500
2	FORD	Ranger	5000
```

```lambda``` function can also be applied for simplicity:

```py
df['model'] = df['model'].apply(lambda x: x.lower())
```
```
make	model	ENGIN-VOLUME
0	NISSAN	skyline	3000
1	PORSCHE	911	3500
2	FORD	ranger	5000
```

```apply``` can be used on DataFrame as well. If we say:

```py
df.apply(pd.Series.min)
```
```
make            FORD
model            911
ENGIN-VOLUME    3000
dtype: object
```

Because alphabetically "Ford" is the lowest value.<br>
This would make more sense, of course, with numeric values.

Lambda works with series so:

```py
df.apply(lambda x: x.max())
```
The ```x``` is a Series - and not a value.
```
make            PORSCHE
model           skyline
ENGIN-VOLUME       5000
dtype: object
```

<br>

### applymap
Only works on DataFrames and applies the function on every element of DataFrame.

```py
df.applymap(len)
```
```
	make	model	ENGIN-VOLUME
0	6	7	4
1	7	3	4
2	4	6	4
```

<br>

### map
Works on Series and is used to substitute values in Series object.

```py
df['make'].map({ 'FORD': 'GM', 'TOYOTA': 'Honda' })
```
```
0    NaN
1    NaN
2     GM
Name: make, dtype: object
```

the values it couldn't substitute has been converted to ```NaN```.

<br>

### replace
Does not substitute values which cannot be found:

```py
df['make'].replace({ 'FORD': 'GM', 'TOYOTA': 'Honda' })
```
```
0     NISSAN
1    PORSCHE
2         GM
Name: make, dtype: object
```

<br>

## Apply the knowledge on StackOverflow Survey

Rename columns to a more meaningful text:

```py
df.rename(columns={'ConvertedComp': 'SalaryUSD'})
```

First check the result and if everything looks fine, the apply ```inplace```:

```py
df.rename(columns={'ConvertedComp': 'SalaryUSD'}, inplace=True)
```

We can use ```map``` or ```replace``` to convert the *Yes/No* values to ```boolean``` to make a better data for analysis.

```py
df['Hobbyist'] = df['Hobbyist'].map({ 'Yes': True, 'No': False })
```

