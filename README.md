#importing libraries 
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

#creating dataframe
dataframe = pd.read_csv("D:\Zomato data .csv")
print(dataframe.head())

#ratings
def handleRate(value):
	value=str(value).split('/')
	value=value[0];
	return float(value)

dataframe['rate']=dataframe['rate'].apply(handleRate)
print(dataframe.head())

#for ratings
def handleRate(value):
	value=str(value).split('/')
	value=value[0];
	return float(value)

 #summary of the data frame
dataframe.info()

#listed_in (type) column.
type_counts = dataframe['listed_in(type)'].value_counts()


custom_colors = ['skyblue', 'lightgreen', 'salmon', 'gold']  # Adjust the number of colors to match the categories

sns.countplot(x=dataframe['listed_in(type)'], palette=custom_colors)
plt.xlabel("Type of restaurant")
plt.show()


grouped_data = dataframe.groupby('listed_in(type)')['votes'].sum()
result = pd.DataFrame({'votes': grouped_data})
plt.plot(result, c="blue", marker="o")
plt.xlabel("Type of restaurant", c="red", size=20)
plt.ylabel("Votes", c="violet", size=20)


#max votes
max_votes = dataframe['votes'].max()
restaurant_with_max_votes = dataframe.loc[dataframe['votes'] == max_votes, 'name']

print("Restaurant(s) with the maximum votes:")
print(restaurant_with_max_votes)


#booking of table
sns.countplot(x=dataframe['book_table'])

#to check rating distrubution
rating_counts = dataframe['rate'].value_counts().sort_index()

sns.barplot(x=rating_counts.index, y=rating_counts.values, palette='viridis')
plt.title("Ratings Distribution")
plt.xlabel("Rate")
plt.ylabel("Frequency")
plt.show()

#to check approx cost of two people
couple_data=dataframe['approx_cost(for two people)']
sns.countplot(x=couple_data)

pivot_table = dataframe.pivot_table(index='listed_in(type)', columns='online_order', aggfunc='size', fill_value=0)
sns.heatmap(pivot_table, annot=True, cmap="YlGnBu", fmt='d')
plt.title("Heatmap")
plt.xlabel("Online Order")
plt.ylabel("Listed In (Type)")
plt.show()



 
