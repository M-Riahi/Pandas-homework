# Pandas-homework:
# Dependencies 
import pandas as pd

# load File
file_to_load = "Resources/purchase_data.csv"

# Read Purchasing File and create Data Frame
purchase_data = pd.read_csv(file_to_load)

Player Count: 
#display/set to variable
players = len(purchase_data['SN'].unique())

#set in DF
players_df = pd.DataFrame({"Total # of Players": [len(purchase_data.SN.unique())]})
players_df

Purchasing Analysis (Total)¶:
#Sum up unique elements
unique_items = len(purchase_data['Item ID'].unique())

#look for average price
avg_price= purchase_data['Price'].mean()

#Sum up number of purchases
total_purchases= len(purchase_data['Purchase ID'])

#Determine the total revenue from all sales
total_revenue= sum(purchase_data['Price'])

#print dataframe with outcome
summary_df = pd.DataFrame({
    'Unique items': unique_items,
    'Average Price': '${:.2f}'.format(avg_price),
    'Total Purchases': total_purchases,
    'Total Revenue': '${:.2f}'.format(total_revenue)
},index=[0])
summary_df

Gender Demographics:

# Gender Distribution
gender_count = gender['Gender'].value_counts()

#Gender Percentage
gender_percent = (gender['Gender'].value_counts()/players)*100

#print outcome in dataframe
gender_df = pd.DataFrame({
    'Count': gender_count,
    'Percent of Total Players': gender_percent.map('{:.2f}%'.format)
})
gender_df

Purchasing Analysis (Gender):
#Gender Purchase classification
gender_purchase_data = purchase_data.groupby('Gender')
gender_purchase_count = gender_purchase_data['Gender'].count()
gender_purchase_count #test works

#average purchase pirce
gender_purchase_mean = gender_purchase_data['Price'].mean()
gender_purchase_mean #test works

#total revenue
gender_purchase_total = gender_purchase_data['Price'].sum()
gender_purchase_total #test works

Age Demographics:
#age bins
bins = [0, 9, 14, 19, 24, 29, 34, 39, 1000]

group_labels = ['<10', '10-14', '15-19', '20-24', '25-29', '30-34', '35-39', '40+']
#categorize the existing players using the age bins
purchase_data['age_group'] =  pd.cut(purchase_data['Age'], bins, labels=group_labels)
#groupby_age
players_by_age = purchase_data.groupby('age_group').SN.nunique()

#create dataframe with percentage and count of total players for each group
age_demo = pd.DataFrame({
    'Total Count': players_by_age,
    'Percentage of Players': (players_by_age / purchase_data.SN.nunique() * 100).map("{:.2f}".format)
})
age_demo



