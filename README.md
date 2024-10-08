# Zomato-Data-Analysis
An analysis of Zomato restaurant and customer data to uncover trends and insights. This project explores dining preferences, restaurant ratings, and customer behavior to provide actionable business insights.
#Importing Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
df= pd.read_csv("Zomato data .csv")
# print(df)
df.head()
#Data Cleaning
#Remove /5 from rating rate
def handlerate(value):
    value= str(value).split("/")
    value=value[0]
    return float(value)
df["rate"]=df["rate"].apply(handlerate) 
df.head()
df.info()
#Type of Restourant
sns.countplot(x=df['listed_in(type)'])
plt.xlabel("Type of Resturant")
#conclusion-Maximum order from dining category
![image](https://github.com/user-attachments/assets/5e8f13a8-2a6c-475c-826f-dcbf98e213bd)
#Which restourant got highest votes
grouped_data = df.groupby('listed_in(type)')['votes'].sum()
result = pd.DataFrame({'votes': grouped_data})  # Use DataFrame instead of df
plt.plot(result, c="blue", marker="o")
plt.xlabel("Type of restaurant", c="red", size=10)
plt.ylabel("Votes", c="red", size=10)
#Dining Resturant got maximum votes
![image](https://github.com/user-attachments/assets/af5b507d-d106-4d0f-a206-0f36dca01fde)
plt.hist(df["rate"],bins= 5)
plt.title("Rating Distribution")
plt.show()
# Majority Restourants got rating 3.5 to 4
![image](https://github.com/user-attachments/assets/5557b2ab-e892-4850-95aa-1475ce5bb65f)
#Average order spent by couple
sns.countplot(x=df["approx_cost(for two people)"])
plt.show()
Conclusion:Majority of couples prefer resturants with an approx cost of 300 rupees
![image](https://github.com/user-attachments/assets/19305302-dc7d-4e17-b596-5b099300e7cc)
#Which mode receives maximum ratings
# df.head()
plt.figure(figsize= (7,7))
sns.boxplot(x='online_order',y='rate',data= df)
#conclusion: Offline order receives less rating as compare to online order
![image](https://github.com/user-attachments/assets/18f95db2-e3d2-45b7-a189-1917bd49f0ea)
pivot_table = df.pivot_table(index='listed_in(type)', columns='online_order', aggfunc='size', fill_value=0)
sns.heatmap(pivot_table, annot=True, cmap="YlGnBu", fmt='d')
plt.title("Heatmap")
plt.xlabel("Online Order")
plt.ylabel("Listed in type")
plt.show()
#Dining restaurants primarily accept offline orders,whereas cafes primarily receive online orders,
#This suggests that clients prefer orders in person at restaurants,but prefer online ordering at cafes.
![image](https://github.com/user-attachments/assets/0e387efe-f213-44c9-a5e6-3ee3dd878c46)



