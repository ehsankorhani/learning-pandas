# DataFrame and Series data types

They are backbone and primary data types of Pandas.

Data frame is rows and columns of data. It is a 2-dimensional labeled data structure with columns of potentially different types. 

## How to think about DataFrames

It is easier to think about DataFrames as ```dictionaries``` with a ```list``` as value for the keys.

Example:

```py
car = {
    "make": ["Nissan", "Porsche", "BMW"],
    "model": ["Skyline", "911", "M1" ],
    "engin_volume": ["3000", "3500", "4500"]
}
```

and the data can be access with:

```py
car["make"]
# or
car.make
```

TO create a DataFrame with this object (in Jupyter):

```py
import pandas as pd
df = pd.DataFrame(car)
df
```

And the output will be:

```py
	make	model	engin_volume
0	Nissan	Skyline	3000
1	Porsche	911	3500
2	BMW	M1	4500
```

<br>

## Series

It is row of data or a one dimensional array.

Type of data frame we created is of course a DataFrame:

```py
type (df)
pandas.core.frame.DataFrame
```

But if we examine the type of a column:

```py
type (df["make"])
pandas.core.series.Series
```

It's a ```series```.

A ```series``` is list of data, but in addition, it has much more functionality.

<br>

## Access multiple columns

Bracket notation can be used to pass in the *list* of column we want to access.

```py
df[["model", "engin_volume"]]
```

The output is another DataFrame:
```
	model	engin_volume
0	Skyline	3000
1	911	3500
2	M1	4500
```

<br>

## Get columns and rows

TO get a list of columns we can use:

```py
df.columns
```

But to get rows we can use ```loc``` or ```iloc``` indexers.

With ```iloc``` we're looking for an integer location.

```py
df.iloc[0] # integer locator
```

Output:
```
make             Nissan
model           Skyline
engin_volume       3000
Name: 0, dtype: object
```

To get multiple rows:

```py
df.iloc[[0, 1]]
```

To specify the required columns when getting rows:

```py
df.iloc[[0, 2], 2]
```

Second argument is the column. <br>
Single column value will return a ```series``` and list will return another ```DataFrame```.

Output:

```
0    3000
2    4500
Name: engin_volume, dtype: object
```

With ```loc``` we'll looking for a ```label```.

```py
df.loc[[0,1], "model"]
```

Output:
```
0    Skyline
1        911
Name: model, dtype: object
```

In addition, we can use ```slicing``` to pass a range of rows (or columns) we want:

```py
df.loc(0:1, "model")
# or
df.loc(0:1, "model":"build_year") # second argument is inclusive
```

<br>



<br>



<br>