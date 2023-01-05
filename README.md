# Market Analysis in Dublin

## Business Problem
A new city manager for Airbnb has started in Dublin and wants to better understand:
- What guests are searching for in Dublin,
- Which inquiries hosts tend to accept.
- What gaps exist between guest demand and host supply
- Any other information that deepens the understanding of the data

The goal is to analyze, understand, visualize, and communicate the demand/supply of the market in Dublin

## Dataset Used
contacts.tsv and searches.tsv file from AirBnB

## Tools Used
- Pandas
- Numpy
- Seaborn
- Matplotlib.pyplot

# Data Exploration
Columns of both datasets

![image](https://user-images.githubusercontent.com/65124287/210721551-c67a3b3c-9cdf-4da0-b07d-388a9f5244f7.png)

The neighbourhood column in searches has 96.2336% of null values. This could lead to inaccurate assumptions about the demand from people. When looking through the column, 'City Centre' was a common choice, so this should be investigated further with more data.

## searches Dataset
Using `searches.info()` or `searches.dtypes()`, I can observe that the date columns `ds`, `ds_checkin`, and `ds_checkout` are in object types. I want to convert these columns to DateTime type for easier analysis and manipulation.

To find out how soon people want their rooms, I created a new column `length_preparation` by deducting `ds` from `ds_checkin`. This information might be useful since I can find out how soon people start planning their trips and lead to better business decisions. 


To better understand the dataset and its distribution of values within columns, use `searches.describe()`.
![image](https://user-images.githubusercontent.com/65124287/210722800-3fc9c538-e69d-4566-ba26-05d100873bab.png)

The number of guests is usually 1 or 2. This can be understood since even at 75% the n_guests_min and n_guests_max are 2 and at 25% is 1. Leading me to believe that smaller accommodations are preferred.

## Distribution
1) First, let's start with the minimum and maximum guests. I can find the number of people searched for when booking rooms.
![image](https://user-images.githubusercontent.com/65124287/210723112-20c9ab12-cde3-4aab-b222-3188e0b2666d.png)

Both `n_guests_min` and `n_guests_max` have similar distributions with 1 being the most popular option and 2 being the next popular option.

2) Let's find out when are people making these searches. With this information, I can calculate when people start thinking about going to Dublin for vacation for marketing purposes.

![image](https://user-images.githubusercontent.com/65124287/210723603-80c37611-375c-4364-80f5-e9a4fe1bb7b0.png)

I can observe that all date searches were between October 1st to October 14th. No major variation in when search was conducted between these dates.
Might want to start marketing Dublin as a potential location for vacation during the peak search periods.

3) Let's understand what is the maximum price people are willing to pay for a room.

![image](https://user-images.githubusercontent.com/65124287/210723770-94826821-3105-492e-82d4-eeff9b7f8ada.png)

Most people search for a room below $200/night with most searches around $100/night. 59% of people searched for rooms between $60 and $130 a night.

4) Next, let's calculate how long soon people want rooms when booking.

![image](https://user-images.githubusercontent.com/65124287/210725139-6b4d9df5-8e63-4bd9-97e8-a78435210774.png)

Based on this data, around 37% of people search for a room within 2 weeks
- 23.7% search for rooms within a week
- 13.46% search for rooms between 1-2 weeks
- 12.51% search for rooms between 2-3 weeks

5) Let's find the distribution of the number of nights people want to stay.

![image](https://user-images.githubusercontent.com/65124287/210726702-716b4787-ff4b-4889-94cb-ea126617b99c.png)

Around 70% of people want to stay between 1-4 days, mostly 2 or 3.
People generally don’t want to stay for more than a week (only 15% want to stay more than a week)

6) Let's calculate when people want to take a trip to Dublin. Use the check-in date to calculate this.

![image](https://user-images.githubusercontent.com/65124287/210726900-cb96395c-0148-455a-94be-01b35ba180e5.png)

83.74% of searches were in the October-December.

Breakdown:
- 45.05% in October
- 26.1% in November
- 12.6% in December

7) I want to understand which are the most common type of rooms searched for by using `searches['filter_room_types'].unique()[0:15]` to display the first 15 unique values.

Most of the room types requested were entire home/apt and private rooms. Sometimes shared rooms.

On the Airbnb website, there are only 4 values in the type of place:
- Entire Place
- Private Room
- Hotel Room
- Shared Room

8) The origin_country column  indicates which country the search came from. I can find the (top 15) most common countries searched from.

![image](https://user-images.githubusercontent.com/65124287/210728684-36934e75-f79e-4659-9d68-731e0a61de12.png)

Ireland (IE), the United States (US), and Great Britain (GB) comprise 48% of searches. Dublin destinations could be promoted within these 3 countries more for the winter months.

## contacts Dataset
After analyzing the searches dataset, I'll start analyzing the contacts dataset. 

Using `contacts.info()` or `contacts.dtypes()`, I can observe that there are multiple columns to be converted to DateTime datat type.

These columns include:
- `ts_contact_at`
- `ts_reply_at`
- `ts_accepted_at`
- `ts_booking_at`
- `ds_checkin`
- `ds_checkout`
- `accepted`

I also created a new column to indicate the length of stay (`length_stay`) by subtracting `ds_checkin` from `ds_checkout`.

1) Finding the distribution of the number of the guests (`n_guests`) staying.
This would be useful in comparing how many guests were searched for versus how many guests the room was booked for.

![image](https://user-images.githubusercontent.com/65124287/210736066-b3c3db51-8066-4e76-8ab0-d16e0009055c.png)

2 guests is the most popular option to book, but 1 guest is the most popularly searched option (as observed from the search dataset). This leads me to believe there could potentially be a lack of supply of single guest rooms.

As seen from the search dataset during the common check-in dates, the popular dates are October-December.

2) I want to find out if there happen to be major difference between people rejected vs accepted. 

![image](https://user-images.githubusercontent.com/65124287/210736620-f5e15f0f-1cbf-4fc0-99a9-0e7f9399095e.png)

There does not appear to be any major variation between accepted vs rejected users.

3) Merge datasets for more analysis

![image](https://user-images.githubusercontent.com/65124287/210736853-203925c8-fb1a-40f4-b6fd-7f952c08af0b.png)

Let's build a table to quantify the `filter_price_max` visualization.

![image](https://user-images.githubusercontent.com/65124287/210737148-8bcca2e7-3e1a-444b-9071-bdf741b83db4.png)

Based on this table, it can be seen that regardless of `filter_price_max`, people are accepted at similar rates around 43%.

4) I wanted to find out of there are any differences in the acceptance rate by the country of origon of the potential guests. 

![image](https://user-images.githubusercontent.com/65124287/210737706-1608bb98-3cf7-47dd-ba53-c3ca47c17d91.png)

India (IN) has the lowest acceptance rate of 15%, which is half of the acceptance rate compared to the second lowest accepted country, Croatia (HR).

Denmark (DK) has the highest acceptance rate but low application numbers. Might want to consider increasing marketing to lead to higher demand.
