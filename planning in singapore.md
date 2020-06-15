```python
import pandas as pd
data = pd.read_html('https://en.wikipedia.org/wiki/Planning_Areas_of_Singapore',skiprows=1)
df = data[1]
df.columns=['Neighborhood','Malay', 'Chinese','Pinyin','Tamil','Region','Area','Population','Density']
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>Malay</th>
      <th>Chinese</th>
      <th>Pinyin</th>
      <th>Tamil</th>
      <th>Region</th>
      <th>Area</th>
      <th>Population</th>
      <th>Density</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bedok</td>
      <td>*</td>
      <td>勿洛</td>
      <td>Wù luò</td>
      <td>பிடோக்</td>
      <td>East</td>
      <td>21.69</td>
      <td>279380</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bishan</td>
      <td>NaN</td>
      <td>碧山</td>
      <td>Bì shān</td>
      <td>பீஷான்</td>
      <td>Central</td>
      <td>7.62</td>
      <td>88010</td>
      <td>12000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Boon Lay</td>
      <td>NaN</td>
      <td>文礼</td>
      <td>Wén lǐ</td>
      <td>பூன் லே</td>
      <td>West</td>
      <td>8.23</td>
      <td>30</td>
      <td>3.6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bukit Batok</td>
      <td>*</td>
      <td>武吉巴督</td>
      <td>Wǔjí bā dū</td>
      <td>புக்கிட் பாத்தோக்</td>
      <td>West</td>
      <td>11.13</td>
      <td>153740</td>
      <td>14000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bukit Merah</td>
      <td>*</td>
      <td>红山</td>
      <td>Hóng shān</td>
      <td>புக்கிட் மேரா</td>
      <td>Central</td>
      <td>14.34</td>
      <td>151980</td>
      <td>11000</td>
    </tr>
  </tbody>
</table>
</div>




```python
select_columns = ['Neighborhood','Region','Area','Population','Density']
df = df[select_columns]
df = df[df.Region == 'East']
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>Region</th>
      <th>Area</th>
      <th>Population</th>
      <th>Density</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bedok</td>
      <td>East</td>
      <td>21.69</td>
      <td>279380</td>
      <td>13000</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Changi</td>
      <td>East</td>
      <td>40.61</td>
      <td>1830</td>
      <td>80.62</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Changi Bay</td>
      <td>East</td>
      <td>1.70</td>
      <td>*</td>
      <td>*</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Pasir Ris</td>
      <td>East</td>
      <td>15.02</td>
      <td>148020</td>
      <td>9600</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Paya Lebar</td>
      <td>East</td>
      <td>11.69</td>
      <td>40</td>
      <td>3.4</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Tampines</td>
      <td>East</td>
      <td>20.89</td>
      <td>256730</td>
      <td>12400</td>
    </tr>
  </tbody>
</table>
</div>




```python
latitudes = [1.323608, 1.3450101, 1.3219708, 1.3720937, 1.3516087, 1.3495907]
longitudes = [103.9273405, 103.9832089, 104.0290022, 103.9473728, 103.8995160, 103.9567879]
df['Latitude'] = pd.Series(latitudes, index=df.index)
df['Longitude'] = pd.Series(longitudes, index=df.index)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>Region</th>
      <th>Area</th>
      <th>Population</th>
      <th>Density</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bedok</td>
      <td>East</td>
      <td>21.69</td>
      <td>279380</td>
      <td>13000</td>
      <td>1.323608</td>
      <td>103.927340</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Changi</td>
      <td>East</td>
      <td>40.61</td>
      <td>1830</td>
      <td>80.62</td>
      <td>1.345010</td>
      <td>103.983209</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Changi Bay</td>
      <td>East</td>
      <td>1.70</td>
      <td>*</td>
      <td>*</td>
      <td>1.321971</td>
      <td>104.029002</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Pasir Ris</td>
      <td>East</td>
      <td>15.02</td>
      <td>148020</td>
      <td>9600</td>
      <td>1.372094</td>
      <td>103.947373</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Paya Lebar</td>
      <td>East</td>
      <td>11.69</td>
      <td>40</td>
      <td>3.4</td>
      <td>1.351609</td>
      <td>103.899516</td>
    </tr>
  </tbody>
</table>
</div>




```python

import pandas as pd # library for data analsysis
pd.set_option('display.max_columns', None)
pd.set_option('display.max_rows', None)

import json # library to handle JSON files

#!conda install -c conda-forge geopy --yes # uncomment this line if you haven't completed the Foursquare API lab
from geopy.geocoders import Nominatim # convert an address into latitude and longitude values

import requests # library to handle requests
from pandas.io.json import json_normalize # tranform JSON file into a pandas dataframe

# Matplotlib and associated plotting modules
import matplotlib.cm as cm
import matplotlib.colors as colors

# import k-means from clustering stage
from sklearn.cluster import KMeans

#!conda install -c conda-forge folium=0.5.0 --yes # uncomment this line if you haven't completed the Foursquare API lab
import folium # map rendering library

print('Libraries imported.')
```

    Libraries imported.



```python
CLIENT_ID = '' # your Foursquare ID
CLIENT_SECRET = '' # your Foursquare Secret
VERSION = '20190126' # Foursquare API version

print('Your credentails:')
print('CLIENT_ID: ' + CLIENT_ID)
print('CLIENT_SECRET:' + CLIENT_SECRET)

LIMIT = 100
radius = 500

```

    Your credentails:
    CLIENT_ID: 
    CLIENT_SECRET:



```python
def getNearbyVenues(names, latitudes, longitudes, radius=500):
    
    venues_list=[]
    for name, lat, lng in zip(names, latitudes, longitudes):
        print(name)
            
        # create the API request URL
        url = 'https://api.foursquare.com/v2/venues/explore?&client_id={}&client_secret={}&v={}&ll={},{}&radius={}&limit={}'.format(
            CLIENT_ID, 
            CLIENT_SECRET, 
            VERSION, 
            lat, 
            lng, 
            radius, 
            LIMIT)
            
        # make the GET request
        results = requests.get(url).json()["response"]['groups'][0]['items']
        
        # return only relevant information for each nearby venue
        venues_list.append([(
            name, 
            lat, 
            lng, 
            v['venue']['name'], 
            v['venue']['location']['lat'], 
            v['venue']['location']['lng'],  
            v['venue']['categories'][0]['name']) for v in results])

    nearby_venues = pd.DataFrame([item for venue_list in venues_list for item in venue_list])
    nearby_venues.columns = ['Neighborhood', 
                  'Neighborhood Latitude', 
                  'Neighborhood Longitude', 
                  'Venue', 
                  'Venue Latitude', 
                  'Venue Longitude', 
                  'Venue Category']
    
    return(nearby_venues)
```


```python

singapore_venues = getNearbyVenues(names=df['Neighborhood'],
                                   latitudes=df['Latitude'],
                                   longitudes=df['Longitude']
                                  )
```

    Bedok
    Changi
    Changi Bay
    Pasir Ris
    Paya Lebar
    Tampines



```python
singapore_venues.shape

```




    (113, 7)




```python
singapore_venues.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>Neighborhood Latitude</th>
      <th>Neighborhood Longitude</th>
      <th>Venue</th>
      <th>Venue Latitude</th>
      <th>Venue Longitude</th>
      <th>Venue Category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bedok</td>
      <td>1.323608</td>
      <td>103.92734</td>
      <td>Ya Kun Kaya Toast 亞坤</td>
      <td>1.324095</td>
      <td>103.929198</td>
      <td>Coffee Shop</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bedok</td>
      <td>1.323608</td>
      <td>103.92734</td>
      <td>FairPrice Fínest</td>
      <td>1.324140</td>
      <td>103.929260</td>
      <td>Supermarket</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bedok</td>
      <td>1.323608</td>
      <td>103.92734</td>
      <td>Haidilao Hot Pot 海底捞火锅</td>
      <td>1.324299</td>
      <td>103.929104</td>
      <td>Hotpot Restaurant</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bedok</td>
      <td>1.323608</td>
      <td>103.92734</td>
      <td>Bedok Chwee Kueh 勿洛水粿</td>
      <td>1.324903</td>
      <td>103.930250</td>
      <td>Chinese Restaurant</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bedok</td>
      <td>1.323608</td>
      <td>103.92734</td>
      <td>Song Zhou Luo Bo Gao 松洲箩卜糕</td>
      <td>1.324836</td>
      <td>103.930520</td>
      <td>Breakfast Spot</td>
    </tr>
  </tbody>
</table>
</div>




```python
singapore_venues.groupby('Neighborhood').count()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood Latitude</th>
      <th>Neighborhood Longitude</th>
      <th>Venue</th>
      <th>Venue Latitude</th>
      <th>Venue Longitude</th>
      <th>Venue Category</th>
    </tr>
    <tr>
      <th>Neighborhood</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bedok</th>
      <td>61</td>
      <td>61</td>
      <td>61</td>
      <td>61</td>
      <td>61</td>
      <td>61</td>
    </tr>
    <tr>
      <th>Changi</th>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
      <td>12</td>
    </tr>
    <tr>
      <th>Changi Bay</th>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
      <td>5</td>
    </tr>
    <tr>
      <th>Pasir Ris</th>
      <td>25</td>
      <td>25</td>
      <td>25</td>
      <td>25</td>
      <td>25</td>
      <td>25</td>
    </tr>
    <tr>
      <th>Paya Lebar</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Tampines</th>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python

# one hot encoding
singapore_onehot = pd.get_dummies(singapore_venues[['Venue Category']], prefix="", prefix_sep="")

# add neighborhood column back to dataframe
singapore_onehot['Neighborhood'] = singapore_venues['Neighborhood'] 

# move neighborhood column to the first column
fixed_columns = [singapore_onehot.columns[-1]] + list(singapore_onehot.columns[:-1])
singapore_onehot = singapore_onehot[fixed_columns]

singapore_onehot.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>Accessories Store</th>
      <th>Airport Service</th>
      <th>Airport Terminal</th>
      <th>American Restaurant</th>
      <th>Asian Restaurant</th>
      <th>Bakery</th>
      <th>Boat or Ferry</th>
      <th>Bookstore</th>
      <th>Breakfast Spot</th>
      <th>Bubble Tea Shop</th>
      <th>Burger Joint</th>
      <th>Burrito Place</th>
      <th>Bus Line</th>
      <th>Bus Station</th>
      <th>Cafeteria</th>
      <th>Café</th>
      <th>Chinese Restaurant</th>
      <th>Clothing Store</th>
      <th>Coffee Shop</th>
      <th>Convenience Store</th>
      <th>Dessert Shop</th>
      <th>Diner</th>
      <th>Fast Food Restaurant</th>
      <th>Flower Shop</th>
      <th>Food Court</th>
      <th>French Restaurant</th>
      <th>Fried Chicken Joint</th>
      <th>Frozen Yogurt Shop</th>
      <th>Gastropub</th>
      <th>Grocery Store</th>
      <th>Hobby Shop</th>
      <th>Hong Kong Restaurant</th>
      <th>Hotpot Restaurant</th>
      <th>Housing Development</th>
      <th>Indian Restaurant</th>
      <th>Italian Restaurant</th>
      <th>Japanese Restaurant</th>
      <th>Jewelry Store</th>
      <th>Karaoke Bar</th>
      <th>Korean Restaurant</th>
      <th>Malay Restaurant</th>
      <th>Men's Store</th>
      <th>Military Base</th>
      <th>Movie Theater</th>
      <th>Noodle House</th>
      <th>Outdoor Supply Store</th>
      <th>Pizza Place</th>
      <th>Plaza</th>
      <th>Restaurant</th>
      <th>Road</th>
      <th>Salon / Barbershop</th>
      <th>Sandwich Place</th>
      <th>Shopping Mall</th>
      <th>Soup Place</th>
      <th>South Indian Restaurant</th>
      <th>Sporting Goods Shop</th>
      <th>Supermarket</th>
      <th>Sushi Restaurant</th>
      <th>Tunnel</th>
      <th>Vegetarian / Vegan Restaurant</th>
      <th>Wings Joint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bedok</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bedok</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bedok</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bedok</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Bedok</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python

singapore_grouped = singapore_onehot.groupby('Neighborhood').mean().reset_index()
singapore_grouped.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>Accessories Store</th>
      <th>Airport Service</th>
      <th>Airport Terminal</th>
      <th>American Restaurant</th>
      <th>Asian Restaurant</th>
      <th>Bakery</th>
      <th>Boat or Ferry</th>
      <th>Bookstore</th>
      <th>Breakfast Spot</th>
      <th>Bubble Tea Shop</th>
      <th>Burger Joint</th>
      <th>Burrito Place</th>
      <th>Bus Line</th>
      <th>Bus Station</th>
      <th>Cafeteria</th>
      <th>Café</th>
      <th>Chinese Restaurant</th>
      <th>Clothing Store</th>
      <th>Coffee Shop</th>
      <th>Convenience Store</th>
      <th>Dessert Shop</th>
      <th>Diner</th>
      <th>Fast Food Restaurant</th>
      <th>Flower Shop</th>
      <th>Food Court</th>
      <th>French Restaurant</th>
      <th>Fried Chicken Joint</th>
      <th>Frozen Yogurt Shop</th>
      <th>Gastropub</th>
      <th>Grocery Store</th>
      <th>Hobby Shop</th>
      <th>Hong Kong Restaurant</th>
      <th>Hotpot Restaurant</th>
      <th>Housing Development</th>
      <th>Indian Restaurant</th>
      <th>Italian Restaurant</th>
      <th>Japanese Restaurant</th>
      <th>Jewelry Store</th>
      <th>Karaoke Bar</th>
      <th>Korean Restaurant</th>
      <th>Malay Restaurant</th>
      <th>Men's Store</th>
      <th>Military Base</th>
      <th>Movie Theater</th>
      <th>Noodle House</th>
      <th>Outdoor Supply Store</th>
      <th>Pizza Place</th>
      <th>Plaza</th>
      <th>Restaurant</th>
      <th>Road</th>
      <th>Salon / Barbershop</th>
      <th>Sandwich Place</th>
      <th>Shopping Mall</th>
      <th>Soup Place</th>
      <th>South Indian Restaurant</th>
      <th>Sporting Goods Shop</th>
      <th>Supermarket</th>
      <th>Sushi Restaurant</th>
      <th>Tunnel</th>
      <th>Vegetarian / Vegan Restaurant</th>
      <th>Wings Joint</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bedok</td>
      <td>0.016393</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.032787</td>
      <td>0.00</td>
      <td>0.032787</td>
      <td>0.0</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.016393</td>
      <td>0.049180</td>
      <td>0.065574</td>
      <td>0.016393</td>
      <td>0.065574</td>
      <td>0.016393</td>
      <td>0.032787</td>
      <td>0.00</td>
      <td>0.032787</td>
      <td>0.016393</td>
      <td>0.04918</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.0</td>
      <td>0.032787</td>
      <td>0.00</td>
      <td>0.032787</td>
      <td>0.00</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.032787</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.032787</td>
      <td>0.00</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.016393</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.04918</td>
      <td>0.04918</td>
      <td>0.000000</td>
      <td>0.016393</td>
      <td>0.016393</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Changi</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.166667</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.083333</td>
      <td>0.0</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.083333</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.083333</td>
      <td>0.00000</td>
      <td>0.00000</td>
      <td>0.083333</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Changi Bay</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.8</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.2</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pasir Ris</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.04</td>
      <td>0.040000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.04</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.040000</td>
      <td>0.000000</td>
      <td>0.080000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.04</td>
      <td>0.080000</td>
      <td>0.040000</td>
      <td>0.08000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.04</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.04</td>
      <td>0.040000</td>
      <td>0.04</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.04</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.04</td>
      <td>0.000000</td>
      <td>0.04</td>
      <td>0.080000</td>
      <td>0.040000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.08000</td>
      <td>0.04000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Paya Lebar</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.500000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.5</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.00</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.00000</td>
      <td>0.00000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
singapore_grouped.shape
```




    (6, 63)




```python
import numpy as np
```


```python
def return_most_common_venues(row, num_top_venues):
    row_categories = row.iloc[1:]
    row_categories_sorted = row_categories.sort_values(ascending=False)
    
    return row_categories_sorted.index.values[0:num_top_venues]
```


```python
num_top_venues = 10

indicators = ['st', 'nd', 'rd']

# create columns according to number of top venues
areaColumns = ['Neighborhood']
freqColumns = []
for ind in np.arange(num_top_venues):
    try:
        freqColumns.append('{}{} Most Common Venue'.format(ind+1, indicators[ind]))
    except:
        freqColumns.append('{}th Most Common Venue'.format(ind+1))
columns = areaColumns+freqColumns
# create a new dataframe
neighborhoods_venues_sorted = pd.DataFrame(columns=columns)

neighborhoods_venues_sorted['Neighborhood'] = singapore_grouped['Neighborhood']

for ind in np.arange(singapore_grouped.shape[0]):
    row_categories = singapore_grouped.iloc[ind, :].iloc[3:]
    row_categories_sorted = row_categories.sort_values(ascending=False)
    neighborhoods_venues_sorted.iloc[ind, 1:] = row_categories_sorted.index.values[0:num_top_venues]

neighborhoods_venues_sorted.sort_values(freqColumns, inplace=True)
neighborhoods_venues_sorted
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>1st Most Common Venue</th>
      <th>2nd Most Common Venue</th>
      <th>3rd Most Common Venue</th>
      <th>4th Most Common Venue</th>
      <th>5th Most Common Venue</th>
      <th>6th Most Common Venue</th>
      <th>7th Most Common Venue</th>
      <th>8th Most Common Venue</th>
      <th>9th Most Common Venue</th>
      <th>10th Most Common Venue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Changi Bay</td>
      <td>Boat or Ferry</td>
      <td>Military Base</td>
      <td>Wings Joint</td>
      <td>Chinese Restaurant</td>
      <td>Frozen Yogurt Shop</td>
      <td>Fried Chicken Joint</td>
      <td>French Restaurant</td>
      <td>Food Court</td>
      <td>Flower Shop</td>
      <td>Fast Food Restaurant</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Changi</td>
      <td>Bus Station</td>
      <td>Airport Terminal</td>
      <td>Road</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Men's Store</td>
      <td>Movie Theater</td>
      <td>Airport Service</td>
      <td>Tunnel</td>
      <td>Sporting Goods Shop</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Bedok</td>
      <td>Coffee Shop</td>
      <td>Chinese Restaurant</td>
      <td>Sushi Restaurant</td>
      <td>Supermarket</td>
      <td>Café</td>
      <td>Food Court</td>
      <td>Bakery</td>
      <td>Malay Restaurant</td>
      <td>Noodle House</td>
      <td>Japanese Restaurant</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Pasir Ris</td>
      <td>Food Court</td>
      <td>Fast Food Restaurant</td>
      <td>Supermarket</td>
      <td>Coffee Shop</td>
      <td>Sandwich Place</td>
      <td>Outdoor Supply Store</td>
      <td>Flower Shop</td>
      <td>Diner</td>
      <td>Chinese Restaurant</td>
      <td>Italian Restaurant</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Paya Lebar</td>
      <td>Military Base</td>
      <td>Bus Station</td>
      <td>Wings Joint</td>
      <td>Chinese Restaurant</td>
      <td>Frozen Yogurt Shop</td>
      <td>Fried Chicken Joint</td>
      <td>French Restaurant</td>
      <td>Food Court</td>
      <td>Flower Shop</td>
      <td>Fast Food Restaurant</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Tampines</td>
      <td>Sandwich Place</td>
      <td>Grocery Store</td>
      <td>South Indian Restaurant</td>
      <td>Housing Development</td>
      <td>Indian Restaurant</td>
      <td>Café</td>
      <td>Fast Food Restaurant</td>
      <td>Plaza</td>
      <td>Dessert Shop</td>
      <td>Clothing Store</td>
    </tr>
  </tbody>
</table>
</div>




```python
# set number of clusters
kclusters = 3

singapore_grouped_clustering = singapore_grouped.drop('Neighborhood', 1)

# run k-means clustering
kmeans = KMeans(n_clusters=kclusters, random_state=0).fit(singapore_grouped_clustering)

# check cluster labels generated for each row in the dataframe
kmeans.labels_[0:100]
```




    array([1, 1, 2, 1, 0, 1], dtype=int32)




```python
# add clustering labels
neighborhoods_venues_sorted.insert(0, 'Cluster Labels', kmeans.labels_)
```


```python

singapore_merged = df

# merge singapore_grouped with singapore_data to add latitude/longitude for each neighborhood
singapore_merged = singapore_merged.join(neighborhoods_venues_sorted.set_index('Neighborhood'), on='Neighborhood')

singapore_merged.head() 
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Neighborhood</th>
      <th>Region</th>
      <th>Area</th>
      <th>Population</th>
      <th>Density</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Cluster Labels</th>
      <th>1st Most Common Venue</th>
      <th>2nd Most Common Venue</th>
      <th>3rd Most Common Venue</th>
      <th>4th Most Common Venue</th>
      <th>5th Most Common Venue</th>
      <th>6th Most Common Venue</th>
      <th>7th Most Common Venue</th>
      <th>8th Most Common Venue</th>
      <th>9th Most Common Venue</th>
      <th>10th Most Common Venue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bedok</td>
      <td>East</td>
      <td>21.69</td>
      <td>279380</td>
      <td>13000</td>
      <td>1.323608</td>
      <td>103.927340</td>
      <td>2</td>
      <td>Coffee Shop</td>
      <td>Chinese Restaurant</td>
      <td>Sushi Restaurant</td>
      <td>Supermarket</td>
      <td>Café</td>
      <td>Food Court</td>
      <td>Bakery</td>
      <td>Malay Restaurant</td>
      <td>Noodle House</td>
      <td>Japanese Restaurant</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Changi</td>
      <td>East</td>
      <td>40.61</td>
      <td>1830</td>
      <td>80.62</td>
      <td>1.345010</td>
      <td>103.983209</td>
      <td>1</td>
      <td>Bus Station</td>
      <td>Airport Terminal</td>
      <td>Road</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Men's Store</td>
      <td>Movie Theater</td>
      <td>Airport Service</td>
      <td>Tunnel</td>
      <td>Sporting Goods Shop</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Changi Bay</td>
      <td>East</td>
      <td>1.70</td>
      <td>*</td>
      <td>*</td>
      <td>1.321971</td>
      <td>104.029002</td>
      <td>1</td>
      <td>Boat or Ferry</td>
      <td>Military Base</td>
      <td>Wings Joint</td>
      <td>Chinese Restaurant</td>
      <td>Frozen Yogurt Shop</td>
      <td>Fried Chicken Joint</td>
      <td>French Restaurant</td>
      <td>Food Court</td>
      <td>Flower Shop</td>
      <td>Fast Food Restaurant</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Pasir Ris</td>
      <td>East</td>
      <td>15.02</td>
      <td>148020</td>
      <td>9600</td>
      <td>1.372094</td>
      <td>103.947373</td>
      <td>1</td>
      <td>Food Court</td>
      <td>Fast Food Restaurant</td>
      <td>Supermarket</td>
      <td>Coffee Shop</td>
      <td>Sandwich Place</td>
      <td>Outdoor Supply Store</td>
      <td>Flower Shop</td>
      <td>Diner</td>
      <td>Chinese Restaurant</td>
      <td>Italian Restaurant</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Paya Lebar</td>
      <td>East</td>
      <td>11.69</td>
      <td>40</td>
      <td>3.4</td>
      <td>1.351609</td>
      <td>103.899516</td>
      <td>0</td>
      <td>Military Base</td>
      <td>Bus Station</td>
      <td>Wings Joint</td>
      <td>Chinese Restaurant</td>
      <td>Frozen Yogurt Shop</td>
      <td>Fried Chicken Joint</td>
      <td>French Restaurant</td>
      <td>Food Court</td>
      <td>Flower Shop</td>
      <td>Fast Food Restaurant</td>
    </tr>
  </tbody>
</table>
</div>




```python
latitude = 1.345010
longitude = 103.927340
map_clusters = folium.Map(location=[latitude, longitude], zoom_start=12)

# set color scheme for the clusters
x = np.arange(kclusters)
ys = [i + x + (i*x)**2 for i in range(kclusters)]
colors_array = cm.rainbow(np.linspace(0, 1, len(ys)))
rainbow = [colors.rgb2hex(i) for i in colors_array]

# add markers to the map
markers_colors = []
for lat, lon, poi, cluster in zip(singapore_merged['Latitude'], singapore_merged['Longitude'], singapore_merged['Neighborhood'], singapore_merged['Cluster Labels']):
    label = folium.Popup(str(poi) + ' Cluster ' + str(cluster), parse_html=True)
    folium.CircleMarker(
        [lat, lon],
        radius=5,
        popup=label,
        color=rainbow[cluster-1],
        fill=True,
        fill_color=rainbow[cluster-1],
        fill_opacity=0.7).add_to(map_clusters)
       
map_clusters
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe src="about:blank" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" data-html=PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVMgPSBmYWxzZTsgTF9OT19UT1VDSCA9IGZhbHNlOyBMX0RJU0FCTEVfM0QgPSBmYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC10aGVtZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9yYXdnaXQuY29tL3B5dGhvbi12aXN1YWxpemF0aW9uL2ZvbGl1bS9tYXN0ZXIvZm9saXVtL3RlbXBsYXRlcy9sZWFmbGV0LmF3ZXNvbWUucm90YXRlLmNzcyIvPgogICAgPHN0eWxlPmh0bWwsIGJvZHkge3dpZHRoOiAxMDAlO2hlaWdodDogMTAwJTttYXJnaW46IDA7cGFkZGluZzogMDt9PC9zdHlsZT4KICAgIDxzdHlsZT4jbWFwIHtwb3NpdGlvbjphYnNvbHV0ZTt0b3A6MDtib3R0b206MDtyaWdodDowO2xlZnQ6MDt9PC9zdHlsZT4KICAgIAogICAgICAgICAgICA8c3R5bGU+ICNtYXBfYmY1ZDZhMzEzNTUyNDZlM2FhMjI0MTIwMWQyMGQ4OTkgewogICAgICAgICAgICAgICAgcG9zaXRpb24gOiByZWxhdGl2ZTsKICAgICAgICAgICAgICAgIHdpZHRoIDogMTAwLjAlOwogICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgICAgICAgICAgdG9wOiAwLjAlOwogICAgICAgICAgICAgICAgfQogICAgICAgICAgICA8L3N0eWxlPgogICAgICAgIAo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgICAgICAgICA8ZGl2IGNsYXNzPSJmb2xpdW0tbWFwIiBpZD0ibWFwX2JmNWQ2YTMxMzU1MjQ2ZTNhYTIyNDEyMDFkMjBkODk5IiA+PC9kaXY+CiAgICAgICAgCjwvYm9keT4KPHNjcmlwdD4gICAgCiAgICAKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGJvdW5kcyA9IG51bGw7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcF9iZjVkNmEzMTM1NTI0NmUzYWEyMjQxMjAxZDIwZDg5OSA9IEwubWFwKAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgJ21hcF9iZjVkNmEzMTM1NTI0NmUzYWEyMjQxMjAxZDIwZDg5OScsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB7Y2VudGVyOiBbMS4zNDUwMSwxMDMuOTI3MzRdLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgem9vbTogMTIsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBtYXhCb3VuZHM6IGJvdW5kcywKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGxheWVyczogW10sCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB3b3JsZENvcHlKdW1wOiBmYWxzZSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGNyczogTC5DUlMuRVBTRzM4NTcKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgfSk7CiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciB0aWxlX2xheWVyXzAzYjI5N2MxNjQ5MDQzYTU5ODdkZmY5NTM3M2M3ZjEwID0gTC50aWxlTGF5ZXIoCiAgICAgICAgICAgICAgICAnaHR0cHM6Ly97c30udGlsZS5vcGVuc3RyZWV0bWFwLm9yZy97en0ve3h9L3t5fS5wbmcnLAogICAgICAgICAgICAgICAgewogICJhdHRyaWJ1dGlvbiI6IG51bGwsCiAgImRldGVjdFJldGluYSI6IGZhbHNlLAogICJtYXhab29tIjogMTgsCiAgIm1pblpvb20iOiAxLAogICJub1dyYXAiOiBmYWxzZSwKICAic3ViZG9tYWlucyI6ICJhYmMiCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwX2JmNWQ2YTMxMzU1MjQ2ZTNhYTIyNDEyMDFkMjBkODk5KTsKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9lYTllN2U4YmYyYTA0YjAyYjRjZjg3NzhhNDcxM2JhMiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzEuMzIzNjA4LDEwMy45MjczNDA1XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiM4MGZmYjQiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjODBmZmI0IiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwX2JmNWQ2YTMxMzU1MjQ2ZTNhYTIyNDEyMDFkMjBkODk5KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzcwMzQxZjdmNWE5YTQ2MTRhOTZmNThlNjQ5ZWIyZGVlID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzYzNzJiODU5ODU0MzQ5YzZhMjE4MGVjZmU1YzI4NzM0ID0gJCgnPGRpdiBpZD0iaHRtbF82MzcyYjg1OTg1NDM0OWM2YTIxODBlY2ZlNWMyODczNCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QmVkb2sgQ2x1c3RlciAyPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF83MDM0MWY3ZjVhOWE0NjE0YTk2ZjU4ZTY0OWViMmRlZS5zZXRDb250ZW50KGh0bWxfNjM3MmI4NTk4NTQzNDljNmEyMTgwZWNmZTVjMjg3MzQpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfZWE5ZTdlOGJmMmEwNGIwMmI0Y2Y4Nzc4YTQ3MTNiYTIuYmluZFBvcHVwKHBvcHVwXzcwMzQxZjdmNWE5YTQ2MTRhOTZmNThlNjQ5ZWIyZGVlKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2NkMmE2NDU0ZWE2NDRhZGVhNWU0ZjAwN2VhMjJhOTU0ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMS4zNDUwMTAxLDEwMy45ODMyMDg5XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiM4MDAwZmYiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjODAwMGZmIiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwX2JmNWQ2YTMxMzU1MjQ2ZTNhYTIyNDEyMDFkMjBkODk5KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2EyMDk3ZGVlZGRmODQ0MDQ4NzQ2YWNhN2UxYmUxMzE5ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2JlNzRlMDMyNzlmODQxMTdiNmFlOWVlNzJmZDg1MzkyID0gJCgnPGRpdiBpZD0iaHRtbF9iZTc0ZTAzMjc5Zjg0MTE3YjZhZTllZTcyZmQ4NTM5MiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+Q2hhbmdpIENsdXN0ZXIgMTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfYTIwOTdkZWVkZGY4NDQwNDg3NDZhY2E3ZTFiZTEzMTkuc2V0Q29udGVudChodG1sX2JlNzRlMDMyNzlmODQxMTdiNmFlOWVlNzJmZDg1MzkyKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2NkMmE2NDU0ZWE2NDRhZGVhNWU0ZjAwN2VhMjJhOTU0LmJpbmRQb3B1cChwb3B1cF9hMjA5N2RlZWRkZjg0NDA0ODc0NmFjYTdlMWJlMTMxOSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81MWE1N2VmOTY1ZjE0MmI5ODhmYzA5MjI5ZjM4YTMzZiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzEuMzIxOTcwOCwxMDQuMDI5MDAyMl0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjODAwMGZmIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF9iZjVkNmEzMTM1NTI0NmUzYWEyMjQxMjAxZDIwZDg5OSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF83OTUwODY0ZjUyMjc0NjQ2ODExZjUxZWE2ODEwMGRmMiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8wZTk0MTFhMWI1OWM0MDk2OTUyN2VlZTAzY2YwM2ZkZSA9ICQoJzxkaXYgaWQ9Imh0bWxfMGU5NDExYTFiNTljNDA5Njk1MjdlZWUwM2NmMDNmZGUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNoYW5naSBCYXkgQ2x1c3RlciAxPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF83OTUwODY0ZjUyMjc0NjQ2ODExZjUxZWE2ODEwMGRmMi5zZXRDb250ZW50KGh0bWxfMGU5NDExYTFiNTljNDA5Njk1MjdlZWUwM2NmMDNmZGUpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNTFhNTdlZjk2NWYxNDJiOTg4ZmMwOTIyOWYzOGEzM2YuYmluZFBvcHVwKHBvcHVwXzc5NTA4NjRmNTIyNzQ2NDY4MTFmNTFlYTY4MTAwZGYyKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2EyYjU5NWFmZGE0ZTQzZGJiY2U0ZGFhMGFhY2JjNDI1ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMS4zNzIwOTM3LDEwMy45NDczNzI4XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiM4MDAwZmYiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjODAwMGZmIiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwX2JmNWQ2YTMxMzU1MjQ2ZTNhYTIyNDEyMDFkMjBkODk5KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2NlMjdiNmI1ZmFkMDQ1OTRhZjY4NzZlZTliZTkwZGNkID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2JjYjgzMWM0NzJjODQzOTRiMWNmZmFmY2JlOTgyOTI3ID0gJCgnPGRpdiBpZD0iaHRtbF9iY2I4MzFjNDcyYzg0Mzk0YjFjZmZhZmNiZTk4MjkyNyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+UGFzaXIgUmlzIENsdXN0ZXIgMTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfY2UyN2I2YjVmYWQwNDU5NGFmNjg3NmVlOWJlOTBkY2Quc2V0Q29udGVudChodG1sX2JjYjgzMWM0NzJjODQzOTRiMWNmZmFmY2JlOTgyOTI3KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2EyYjU5NWFmZGE0ZTQzZGJiY2U0ZGFhMGFhY2JjNDI1LmJpbmRQb3B1cChwb3B1cF9jZTI3YjZiNWZhZDA0NTk0YWY2ODc2ZWU5YmU5MGRjZCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9hODFjNzE0OTY3YzM0YzcxYjI5OWI2NjlhNTczM2M2OSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzEuMzUxNjA4NywxMDMuODk5NTE2XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiNmZjAwMDAiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjZmYwMDAwIiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwX2JmNWQ2YTMxMzU1MjQ2ZTNhYTIyNDEyMDFkMjBkODk5KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2U5ZDc1YjIyYjE4OTQxNDc4MjlmMDk2YWZiMTU5NGI1ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2ZiNzlhMzQ4OTk3ZDRjYmFiYzkzN2I5YTMyMDY0YTc1ID0gJCgnPGRpdiBpZD0iaHRtbF9mYjc5YTM0ODk5N2Q0Y2JhYmM5MzdiOWEzMjA2NGE3NSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+UGF5YSBMZWJhciBDbHVzdGVyIDA8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2U5ZDc1YjIyYjE4OTQxNDc4MjlmMDk2YWZiMTU5NGI1LnNldENvbnRlbnQoaHRtbF9mYjc5YTM0ODk5N2Q0Y2JhYmM5MzdiOWEzMjA2NGE3NSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9hODFjNzE0OTY3YzM0YzcxYjI5OWI2NjlhNTczM2M2OS5iaW5kUG9wdXAocG9wdXBfZTlkNzViMjJiMTg5NDE0NzgyOWYwOTZhZmIxNTk0YjUpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNDU0ZDUwYjg0NzhmNDgwYWEzMTJmZGNlYWM3OTI3YzggPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFsxLjM0OTU5MDcsMTAzLjk1Njc4NzldLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiIzgwMDBmZiIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiM4MDAwZmYiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfYmY1ZDZhMzEzNTUyNDZlM2FhMjI0MTIwMWQyMGQ4OTkpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMjlhZTQ1MWYzNWM1NGE2MTk4YTgxZjBjY2RlMWQ1MmYgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfOTg3YmYxZjM5MzIyNDg1M2EzYWFhNmQxNGEzMzg5MjcgPSAkKCc8ZGl2IGlkPSJodG1sXzk4N2JmMWYzOTMyMjQ4NTNhM2FhYTZkMTRhMzM4OTI3IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5UYW1waW5lcyBDbHVzdGVyIDE8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzI5YWU0NTFmMzVjNTRhNjE5OGE4MWYwY2NkZTFkNTJmLnNldENvbnRlbnQoaHRtbF85ODdiZjFmMzkzMjI0ODUzYTNhYWE2ZDE0YTMzODkyNyk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl80NTRkNTBiODQ3OGY0ODBhYTMxMmZkY2VhYzc5MjdjOC5iaW5kUG9wdXAocG9wdXBfMjlhZTQ1MWYzNWM1NGE2MTk4YTgxZjBjY2RlMWQ1MmYpOwoKICAgICAgICAgICAgCiAgICAgICAgCjwvc2NyaXB0Pg== onload="this.contentDocument.open();this.contentDocument.write(atob(this.getAttribute('data-html')));this.contentDocument.close();" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>




```python

```




    Text(0.5, 0, 'Years')




![png](output_20_1.png)



```python

```
