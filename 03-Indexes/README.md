# Indexes

Every DataFrame has a column (on the far left) without a name. That columns is the **index**.

```
	make	model	engin_volume	plate_no
0	Nissan	Skyline	3000	CMZ10AQ
1	Porsche	911	3500	ABC12RR
2	BMW	M1	4500	PLF99AZ
```

Sometimes it makes sense to define a different identifier for each row. That will be the ```label``` for that row.

Although, Pandas doesn't enforce unique values for labels, they will be unique most of the times.

In the example above we can take *Plate No.* as the label since it will be a unique value. TO do that we can say:

```py
df.set_index('plate_no')
```

Output:

```
	        make	model	engin_volume
plate_no			
CMZ10AQ     Nissan	Skyline	3000
ABC12RR     Porsche	911	    3500
PLF99AZ     BMW	    M1      4500
```

This still has not changed the DataFrame:

```py
df
```

Output:
```
	make	model	engin_volume	plate_no
0	Nissan	Skyline	3000	CMZ10AQ
1	Porsche	911	3500	ABC12RR
2	BMW	M1	4500	PLF99AZ
```

To do that we have to explicitly tell Pandas to set this index in place:

```py
df.set_index('plate_no', inplace=True)
```

Then we can check the DataFrame index by:

```py
df.index
```

Output:
```
Index(['CMZ10AQ', 'ABC12RR', 'PLF99AZ'], dtype='object', name='plate_no')
```

Now we can search rows by passing a Plate No.:

```py
df.loc["ABC12RR"]
```

Output:
```
make            Porsche
model               911
engin_volume       3500
Name: ABC12RR, dtype: object
```

At this point we cannot use integer index in ```loc``` anymore.

<br>

## Applying index on main data

*Respondent* id seems to be unique. We can use it as the label.

Apart from the ```set_index``` method we can apply this when reading CSV data:

```py
df = pd.read_csv('data/survey_results_public.csv', index_col='Respondent') # index_col is case-sensitive
```

For the *Schema* file, we can set the *Column" to be the indexer.

```py
schema_df = pd.read_csv('data/survey_results_schema.csv', index_col='Column')
```

This way we can easily find the description for each question.

```py
schema_df.loc['DevType']
```

Output:

```
QuestionText    Which of the following describe you? Please se...
Name: DevType, dtype: object
```

TO see the full description text:

```py
schema_df.loc['DevType', 'QuestionText']
```

Output:

```
'Which of the following describe you? Please select all that apply.'
```

<br>

## Sort Index

To easier finding data:

```py
schema_df.sort_index()
# or
schema_df.sort_index(ascending=False) # in descending order
```

To affecting the sorting in DataFrame:

```py
schema_df.sort_index(inplace=True)
```