# Add and Remove rows and columns

In this section we'll explore how to add and remove the rows and columns of a DataFrame.

## Adding columns

We juts have a create a column and pass in a series of values that we want that column to have:

```py
import pandas as pd

car = {
    "make": ["Nissan", "Porsche", "BMW"],
    "model": ["Skyline", "911", "M1" ],
    "engin_capacity": ["3000", "3500", "4500"]
}

df = pd.DataFrame(car)
df
```
```
    make	model	engin_capacity
0	Nissan	Skyline	3000
1	Porsche	911	    3500
2	BMW	    M1	    4500
```

This:
```py
df['make'] + ' ' + df['model']
```

Will output:

```
0     Nissan Skyline
1    Porsche 911
2        BMW M1
Name: make, dtype: object
```

So, to create a column that concats make and model we just have to do:

```py
df['description'] = df['make'] + ' ' + df['model']
df
```
```
    make	model	engin_capacity	description
0	Nissan	Skyline	3000        	Nissan Skyline
1	Porsche	911	    3500	        Porsche 911
2	BMW	    M1	    4500	        BMW M1
```

Note that we cannot use *dot notation* and we should use *brackets*.

<br>

## Remove columns

To remove we just have to drop the column(s):

```py
df.drop(columns=['make', 'model'], inplace=True)
```
```
    engin_capacity	description
0	3000	        Nissan Skyline
1	3500	        Porsche 911
2	4500	        BMW M1
```

To reverse this back and get the make and model we have to split the description:

```py
df['description'].str.split(' ', expand=True)
```
```
	0	    1
0	Nissan	Skyline
1	Porsche	911
2	BMW	    M1
```

So we can say:

```py
df[['make', 'model']] = df['description'].str.split(' ', expand=True)
```
```
    engin_capacity	description	    make	model
0	3000	        Nissan Skyline	Nissan	Skyline
1	3500	        Porsche 911	    Porsche	911
2	4500	        BMW M1	        BMW	    M1
```

<br>

## Add Rows

To add a row we can use ```append``` method.

```py
df.append({'make': 'Audi'})
```
```
TypeError: Can only append a dict if ignore_index=True
```

Because our command lacks index, we have to add ```ignore_index=True```:

```py
df.append({'make': 'Audi'}, ignore_index=True)
```
```
	make	model	engin_capacity	description
0	Nissan	Skyline	3000	        Nissan Skyline
1	Porsche	911	    3500	        Porsche 911
2	BMW	    M1	    4500	        BMW M1
3	Audi	NaN	    NaN	            NaN
```

We also can add a whole different DataFrame to our original DataFrame:

```py
carList2 = {
    "make": ["Toyota", "Mitsubishi"],
    "model": ["Supra", "Evo" ],
    "engin_capacity": ["4000", "3000"]
}
df2 = pd.DataFrame(carList2)
df2
```
```
    make	    model	engin_capacity
0	Toyota	    Supra	4000
1	Mitsubishi	Evo	    3000
```

And then append this DataFrame to first one:

```py
df.append(df2, ignore_index=True)
```
```
	make	    model	engin_capacity	description
0	Nissan	    Skyline	3000	        Nissan Skyline
1	Porsche	    911	3   500	            Porsche 911
2	BMW	        M1	    4500	        BMW M1
3	Toyota	    Supra	4000	        NaN
4	Mitsubishi	Evo	    3000	        NaN
```

These changes are not permanent unless we re-assign them to original DataFrame:

```
df = df.append(df2, ignore_index=True)
```

> ```append``` doesn't have a ```inplace``` argument as ```drop``` has.

<br>

## Remove Rows

The ```drop``` method can be used to delete a row by index:

```py
df.drop(index=4)
```
```
	make	    model	engin_capacity	description
0	Nissan	    Skyline	3000	        Nissan Skyline
1	Porsche	    911	3   500	            Porsche 911
2	BMW	        M1	    4500	        BMW M1
3	Toyota	    Supra	4000	        NaN
```

And of course, the ```inpalce=True``` is needed to make the change permanent.

<br>

### Remove by condition

We can use ```loc``` or ```drop``` for this reason.

```py
df.drop(index=df[df['make'] == 'Nissan'].index)
```

The better practice to write a cleaner code by separating the definitions:

```py
filt = pd.isna(df['description'])
df.drop(index=df[filt].index)
```
```
	make	model	engin_capacity	description
0	Nissan	Skyline	3000	        Nissan Skyline
1	Porsche	911	    3500	        Porsche 911
2	BMW	    M1	    4500	        BMW M1
```
