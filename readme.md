# Exploratory Data Analysis using SQL.


In this project I use SQL to perform EDA on [this]('HospitalER.csv') data and Seaborn is used for visualization.

We first load the ipython-sql library into the notebook. Then configure it to return pandas DataFrame and finally we connect to the mysql server.
```
#load sql library
%load_ext sql

#configure sql cell function to return pandas DataFrame.
%config SqlMagic.autopandas = True

#Connect to mysql server
%sql mysql+pymysql://root@localhost/
```

To load data to a database you can check the code in the notebook.


To query the database we just use sql magic function like below:
```
%%sql 
Select *
FROM hospital_er
LIMIT 5
```

To store the query results to a variable that we can access for visualization:
```
df = %sql select monthname(date) as Month, \
count(patient_id) AS Count \
from hospital_er \
group by monthname(date) \
order by 1, 2 desc
```

To visualize the data e.g using seaborn alias sns:

```
sns.barplot(data=df, x='Month',y='Count')
```