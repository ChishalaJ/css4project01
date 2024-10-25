# css4project01
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Wed Oct 23 10:21:34 2024

@author: josephine
"""

import pandas as pd
df=pd.read_csv("movie_dataset.csv")

x = df["Metascore"].mean()

df["Metascore"].fillna(x, inplace = True)

x = df["Revenue (Millions)"].mean()

df["Revenue (Millions)"].fillna(x, inplace = True)

#To replace the column names with words without spaces
#df.columns.values[5] = 'Revenue_(Millions)'
df.columns=df.columns.str.replace("Revenue (Millions)","Revenue_Millions")
df.columns=df.columns.str.replace("Runtime (Minutes)","Runtime_Minutes")
#df.columns=df.columns.str.replace(' ','_')


#Q1:Sort the data in ascending orderof Rating to get the highest rated

Sorted_df = df.sort_values(by= 'Rating', ascending=False)
print(Sorted_df)
#Q2:To calculate the average
avg_revenue=df["Revenue_Millions"].mean()

#Q3: Filtering only the 2015 - 2017 data then calculate the mean revenues
New_years = df[(df["Year"] >= 2015) & (df ["Year"] <= 2017)]
print(New_years)
avg_revenue_years=New_years["Revenue_Millions"].mean()

#Q4: Number of movies released in 2016 only
df_2016 =  df[(df["Year"] >= 2016)]
print(len(df_2016))

#Q5: Number of movies by Chrstopher Nolan
Movie_Chris = df[(df["Director"] == 'Christopher Nolan')]
print(len(Movie_Chris))

#Q6: Number Ratings above 8
df_8rating = df[(df["Rating"] >= 8)]
print(len(df_8rating))

#Q7: Median rating for Chris
median_revenue_Chris=Movie_Chris["Rating"].median()
print(median_revenue_Chris)

#Q8: Average ratings for the years
df_2006 =  df[(df["Year"] == 2006)]
avg_revenue_2006=df_2006["Rating"].mean()
print(avg_revenue_2006)
df_2007 =  df[(df["Year"] == 2007)]
avg_revenue_2007=df_2007["Rating"].mean()
print(avg_revenue_2007)

df_2008 =  df[(df["Year"] == 2008)]
avg_revenue_2008=df_2008["Rating"].mean()
print(avg_revenue_2008)

df_2016 =  df[(df["Year"] == 2016)]
avg_revenue_2016=df_2016["Rating"].mean()
print(avg_revenue_2016)

#Q9: Percentage Increase between 2006 - 2016
Percent_Increase = ((len(df_2016) - len(df_2006)) / len(df_2006))*100
print(Percent_Increase)

#Q10: Determine the most common actor in movies, first split the actor entries
df['Actors'] = df['Actors'].str.split(',',)
df_New_Actors = df.explode('Actors').reset_index(drop=True)
mode_Actors= df_New_Actors["Actors"].mode()
print(mode_Actors)
print(len(df_New_Actors[(df_New_Actors["Actors"] == 'Mark Wahlberg')]))
print(len(df_New_Actors[(df_New_Actors["Actors"] == 'Christian Bale')]))

#Q11: To determine the number of unique entry in Genre after spliting each Genre in single row
df['Genre'] = df['Genre'].str.split(',',)
df_New_Genre = df.explode('Genre').reset_index(drop=True)
df_Unique = df_New_Genre['Genre'].nunique()
print(df_Unique)



