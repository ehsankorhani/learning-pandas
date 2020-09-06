# Learning Pandas

**Pandas** is a data analysis library for the *Python*.<br>
Pandas is a tool for data wrangling or munging. It is designed for quick and easy data manipulation, reading, aggregation, and visualization.

It take data in a CSV or TSV file or a SQL database and create a Python object with rows and columns called a data frame. The data frame is very similar to a table in statistical software, say Excel or SPSS.

Below is a list of things that can be achieved using Pandas:
* Indexing, manipulating, renaming, sorting, merging data frame
* Update, Add, Delete columns from a data frame
* Impute missing files, handle missing data or NANs
* Plot data with histogram or box plot


<br>

## Table of Contents

0. Install Pandas
1. Getting started
2. DataFrame and Series data types
3. Indexes
4. Filtering
5. Updating Rows and Columns
6. Add and Remove rows and columns

<br>

## Get a sample data to work with

Stack Overflow survey can be good sample to start learning analysis.

Browse to:
https://insights.stackoverflow.com/survey/

And download a Zip file for any year and extract it in your machine.

<br>

## Install Pandas (on Virtual Environment)

Create a new environment:

```bash
$ python3 -m venv pandas_env
```

And activate it:

```bash
$ source pandas_env/bin/activate
```

Install Pandas:

```bash
pip install pandas
```

<br>

## Jupyter Notebook
It's not a necessity to have Jupyter Notebooks. But it allows to see data more easily in the browser.

Install jupyter with:

```bash
$ pip install jupyterlab
```

And run it in a separate terminal - with the same virtual environment. Because the Jupyter will run as long as the terminal is active.:

```bash
$ jupyter notebook
```

In the browser app, create a new Python3 Notebook.<br>
Give it a name (instead of Untitled).

<br>

We are ready to use **Pandas**.

<br>

### References
* [Top 10 Python Libraries for Data Science](https://towardsdatascience.com/top-10-python-libraries-for-data-science-cd82294ec266)
* [Python Pandas Tutorial](hhttps://youtu.be/ZyhVh-qRZPA)