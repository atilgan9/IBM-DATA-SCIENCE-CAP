```python
!conda install lxml --yes

```

    Collecting package metadata (current_repodata.json): done
    Solving environment: done
    
    ## Package Plan ##
    
      environment location: /home/jupyterlab/conda/envs/python
    
      added / updated specs:
        - lxml
    
    
    The following packages will be downloaded:
    
        package                    |            build
        ---------------------------|-----------------
        ca-certificates-2020.1.1   |                0         125 KB
        certifi-2020.4.5.1         |           py36_0         155 KB
        libxslt-1.1.33             |       h7d1a2b0_0         426 KB
        lxml-4.5.0                 |   py36hefd8a0e_0         1.4 MB
        openssl-1.1.1g             |       h7b6447c_0         2.5 MB
        ------------------------------------------------------------
                                               Total:         4.6 MB
    
    The following NEW packages will be INSTALLED:
    
      libxslt            pkgs/main/linux-64::libxslt-1.1.33-h7d1a2b0_0
      lxml               pkgs/main/linux-64::lxml-4.5.0-py36hefd8a0e_0
    
    The following packages will be SUPERSEDED by a higher-priority channel:
    
      ca-certificates    conda-forge::ca-certificates-2020.4.5~ --> pkgs/main::ca-certificates-2020.1.1-0
      certifi            conda-forge::certifi-2020.4.5.1-py36h~ --> pkgs/main::certifi-2020.4.5.1-py36_0
      openssl            conda-forge::openssl-1.1.1g-h516909a_0 --> pkgs/main::openssl-1.1.1g-h7b6447c_0
    
    
    
    Downloading and Extracting Packages
    ca-certificates-2020 | 125 KB    | ##################################### | 100% 
    lxml-4.5.0           | 1.4 MB    | ##################################### | 100% 
    openssl-1.1.1g       | 2.5 MB    | ##################################### | 100% 
    certifi-2020.4.5.1   | 155 KB    | ##################################### | 100% 
    libxslt-1.1.33       | 426 KB    | ##################################### | 100% 
    Preparing transaction: done
    Verifying transaction: done
    Executing transaction: done



```python

import pandas as pd

data = pd.read_html('https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M',skiprows=1)
df = data[0]
df.columns=['PostalCode','Borough','Neighborhood']
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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M2A</td>
      <td>Not assigned</td>
      <td>Not assigned</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M3A</td>
      <td>North York</td>
      <td>Parkwoods</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M4A</td>
      <td>North York</td>
      <td>Victoria Village</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Regent Park, Harbourfront</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M6A</td>
      <td>North York</td>
      <td>Lawrence Manor, Lawrence Heights</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = df[df.Borough != 'Not assigned']
df.head(7)
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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>M3A</td>
      <td>North York</td>
      <td>Parkwoods</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M4A</td>
      <td>North York</td>
      <td>Victoria Village</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Regent Park, Harbourfront</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M6A</td>
      <td>North York</td>
      <td>Lawrence Manor, Lawrence Heights</td>
    </tr>
    <tr>
      <th>5</th>
      <td>M7A</td>
      <td>Downtown Toronto</td>
      <td>Queen's Park, Ontario Provincial Government</td>
    </tr>
    <tr>
      <th>7</th>
      <td>M9A</td>
      <td>Etobicoke</td>
      <td>Islington Avenue, Humber Valley Village</td>
    </tr>
    <tr>
      <th>8</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Malvern, Rouge</td>
    </tr>
  </tbody>
</table>
</div>




```python
df[df['Neighborhood'] == 'Not assigned']
def replace(row):
    if row['Neighborhood'] == 'Not assigned':
        row['Neighborhood'] = row['Borough']
    return row

df = df.apply(replace, axis = 1)
df.head(7)
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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>M3A</td>
      <td>North York</td>
      <td>Parkwoods</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M4A</td>
      <td>North York</td>
      <td>Victoria Village</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Regent Park, Harbourfront</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M6A</td>
      <td>North York</td>
      <td>Lawrence Manor, Lawrence Heights</td>
    </tr>
    <tr>
      <th>5</th>
      <td>M7A</td>
      <td>Downtown Toronto</td>
      <td>Queen's Park, Ontario Provincial Government</td>
    </tr>
    <tr>
      <th>7</th>
      <td>M9A</td>
      <td>Etobicoke</td>
      <td>Islington Avenue, Humber Valley Village</td>
    </tr>
    <tr>
      <th>8</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Malvern, Rouge</td>
    </tr>
  </tbody>
</table>
</div>




```python
df = df.groupby(['PostalCode','Borough']).apply(lambda group: ','.join(group['Neighborhood']))
df = df.to_frame()
df = df.rename(columns = {0: 'Neighborhood'}).reset_index()
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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhood</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Malvern, Rouge</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M1C</td>
      <td>Scarborough</td>
      <td>Rouge Hill, Port Union, Highland Creek</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M1E</td>
      <td>Scarborough</td>
      <td>Guildwood, Morningside, West Hill</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M1G</td>
      <td>Scarborough</td>
      <td>Woburn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M1H</td>
      <td>Scarborough</td>
      <td>Cedarbrae</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.shape
```




    (103, 3)




```python
!pip install geocoder
```

    Collecting geocoder
    [?25l  Downloading https://files.pythonhosted.org/packages/4f/6b/13166c909ad2f2d76b929a4227c952630ebaf0d729f6317eb09cbceccbab/geocoder-1.38.1-py2.py3-none-any.whl (98kB)
    [K     |████████████████████████████████| 102kB 6.0MB/s ta 0:00:011
    [?25hCollecting click (from geocoder)
    [?25l  Downloading https://files.pythonhosted.org/packages/d2/3d/fa76db83bf75c4f8d338c2fd15c8d33fdd7ad23a9b5e57eb6c5de26b430e/click-7.1.2-py2.py3-none-any.whl (82kB)
    [K     |████████████████████████████████| 92kB 5.0MB/s eta 0:00:011
    [?25hRequirement already satisfied: requests in /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages (from geocoder) (2.23.0)
    Requirement already satisfied: six in /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages (from geocoder) (1.14.0)
    Collecting ratelim (from geocoder)
      Downloading https://files.pythonhosted.org/packages/f2/98/7e6d147fd16a10a5f821db6e25f192265d6ecca3d82957a4fdd592cad49c/ratelim-0.1.6-py2.py3-none-any.whl
    Collecting future (from geocoder)
    [?25l  Downloading https://files.pythonhosted.org/packages/45/0b/38b06fd9b92dc2b68d58b75f900e97884c45bedd2ff83203d933cf5851c9/future-0.18.2.tar.gz (829kB)
    [K     |████████████████████████████████| 829kB 5.3MB/s eta 0:00:01
    [?25hRequirement already satisfied: chardet<4,>=3.0.2 in /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages (from requests->geocoder) (3.0.4)
    Requirement already satisfied: certifi>=2017.4.17 in /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages (from requests->geocoder) (2020.4.5.1)
    Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages (from requests->geocoder) (1.25.9)
    Requirement already satisfied: idna<3,>=2.5 in /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages (from requests->geocoder) (2.9)
    Requirement already satisfied: decorator in /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages (from ratelim->geocoder) (4.4.2)
    Building wheels for collected packages: future
      Building wheel for future (setup.py) ... [?25ldone
    [?25h  Stored in directory: /home/jupyterlab/.cache/pip/wheels/8b/99/a0/81daf51dcd359a9377b110a8a886b3895921802d2fc1b2397e
    Successfully built future
    Installing collected packages: click, ratelim, future, geocoder
    Successfully installed click-7.1.2 future-0.18.2 geocoder-1.38.1 ratelim-0.1.6



```python
df2 = pd.read_csv('http://cocl.us/Geospatial_data')
df2.head()
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
      <th>Postal Code</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1B</td>
      <td>43.806686</td>
      <td>-79.194353</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M1C</td>
      <td>43.784535</td>
      <td>-79.160497</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M1E</td>
      <td>43.763573</td>
      <td>-79.188711</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M1G</td>
      <td>43.770992</td>
      <td>-79.216917</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M1H</td>
      <td>43.773136</td>
      <td>-79.239476</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3 = pd.merge(df, df2, left_on = 'PostalCode', right_on = 'Postal Code', how = 'left')
df3 = df3.drop(columns = ['Postal Code'])
df3.head()
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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhood</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M1B</td>
      <td>Scarborough</td>
      <td>Malvern, Rouge</td>
      <td>43.806686</td>
      <td>-79.194353</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M1C</td>
      <td>Scarborough</td>
      <td>Rouge Hill, Port Union, Highland Creek</td>
      <td>43.784535</td>
      <td>-79.160497</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M1E</td>
      <td>Scarborough</td>
      <td>Guildwood, Morningside, West Hill</td>
      <td>43.763573</td>
      <td>-79.188711</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M1G</td>
      <td>Scarborough</td>
      <td>Woburn</td>
      <td>43.770992</td>
      <td>-79.216917</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M1H</td>
      <td>Scarborough</td>
      <td>Cedarbrae</td>
      <td>43.773136</td>
      <td>-79.239476</td>
    </tr>
  </tbody>
</table>
</div>




```python
df4 = df3[df3['Borough'].str.contains('Toronto')]
df4.head()
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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhood</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>37</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>43.676357</td>
      <td>-79.293031</td>
    </tr>
    <tr>
      <th>41</th>
      <td>M4K</td>
      <td>East Toronto</td>
      <td>The Danforth West, Riverdale</td>
      <td>43.679557</td>
      <td>-79.352188</td>
    </tr>
    <tr>
      <th>42</th>
      <td>M4L</td>
      <td>East Toronto</td>
      <td>India Bazaar, The Beaches West</td>
      <td>43.668999</td>
      <td>-79.315572</td>
    </tr>
    <tr>
      <th>43</th>
      <td>M4M</td>
      <td>East Toronto</td>
      <td>Studio District</td>
      <td>43.659526</td>
      <td>-79.340923</td>
    </tr>
    <tr>
      <th>44</th>
      <td>M4N</td>
      <td>Central Toronto</td>
      <td>Lawrence Park</td>
      <td>43.728020</td>
      <td>-79.388790</td>
    </tr>
  </tbody>
</table>
</div>




```python
import numpy as np 
import json
import requests 
from pandas.io.json import json_normalize

# Matplotlib and associated plotting modules
import matplotlib.cm as cm
import matplotlib.colors as colors

# import k-means from clustering stage
from sklearn.cluster import KMeans

#!conda install -c conda-forge folium=0.5.0 --yes # uncomment this line if you haven't completed the Foursquare API lab
import folium

print('Libraries imported.')
```

    Libraries imported.



```python
CLIENT_ID = 'xxxxxxx' # your Foursquare ID
CLIENT_SECRET = 'xxxxxxxx' # your Foursquare Secret
VERSION = '20190126' # Foursquare API version

print('Your credentails:')
print('CLIENT_ID: ' + CLIENT_ID)
print('CLIENT_SECRET:' + CLIENT_SECRET)


```

    Your credentails:
    CLIENT_ID: xxxxxxxx
    CLIENT_SECRET:xxxxxxxxxx


```python
radius = 500
LIMIT = 100

venues = []

for Latitude, long, post, borough, neighborhood in zip(df4['Latitude'], df4['Longitude'], df4['PostalCode'], df4['Borough'], df4['Neighborhood']):
    url = "https://api.foursquare.com/v2/venues/explore?client_id={}&client_secret={}&v={}&ll={},{}&radius={}&limit={}".format(
        CLIENT_ID,
        CLIENT_SECRET,
        VERSION,
        Latitude,
        long,
        radius, 
        LIMIT)
    
    results = requests.get(url).json()["response"]['groups'][0]['items']
    
    for venue in results:
        venues.append((
            post, 
            borough,
            neighborhood,
            Latitude, 
            long, 
            venue['venue']['name'], 
            venue['venue']['location']['lat'], 
            venue['venue']['location']['lng'],  
            venue['venue']['categories'][0]['name']))
```


```python

venues_df = pd.DataFrame(venues)
venues_df.columns = ['PostalCode', 'Borough', 'Neighborhood', 'BoroughLatitude', 'BoroughLongitude', 'VenueName', 'VenueLatitude', 'VenueLongitude', 'VenueCategory']
print(venues_df.shape)
venues_df.head()
        
```

    (1613, 9)





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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhood</th>
      <th>BoroughLatitude</th>
      <th>BoroughLongitude</th>
      <th>VenueName</th>
      <th>VenueLatitude</th>
      <th>VenueLongitude</th>
      <th>VenueCategory</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>43.676357</td>
      <td>-79.293031</td>
      <td>Glen Manor Ravine</td>
      <td>43.676821</td>
      <td>-79.293942</td>
      <td>Trail</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>43.676357</td>
      <td>-79.293031</td>
      <td>The Big Carrot Natural Food Market</td>
      <td>43.678879</td>
      <td>-79.297734</td>
      <td>Health Food Store</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>43.676357</td>
      <td>-79.293031</td>
      <td>Grover Pub and Grub</td>
      <td>43.679181</td>
      <td>-79.297215</td>
      <td>Pub</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>43.676357</td>
      <td>-79.293031</td>
      <td>Upper Beaches</td>
      <td>43.680563</td>
      <td>-79.292869</td>
      <td>Neighborhood</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M4K</td>
      <td>East Toronto</td>
      <td>The Danforth West, Riverdale</td>
      <td>43.679557</td>
      <td>-79.352188</td>
      <td>MenEssentials</td>
      <td>43.677820</td>
      <td>-79.351265</td>
      <td>Cosmetics Shop</td>
    </tr>
  </tbody>
</table>
</div>




```python
#check to see the unique venues
```


```python
len(venues_df['VenueCategory'].unique())
```




    236



one hot encoding


```python

# one hot encoding
toronto_central_onehot = pd.get_dummies(venues_df[['VenueCategory']], prefix="", prefix_sep="")

# add postal, borough and neighborhood column back to dataframe
toronto_central_onehot['PostalCode'] = venues_df['PostalCode'] 
toronto_central_onehot['Borough'] = venues_df['Borough'] 
toronto_central_onehot['Neighborhoods'] = venues_df['Neighborhood'] 

# move postal, borough and neighborhood column to the first column
fixed_columns = list(toronto_central_onehot.columns[-3:]) + list(toronto_central_onehot.columns[:-3])
toronto_central_onehot = toronto_central_onehot[fixed_columns]

print(toronto_central_onehot.shape)
toronto_central_onehot.head()
```

    (1613, 239)





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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhoods</th>
      <th>Afghan Restaurant</th>
      <th>Airport</th>
      <th>Airport Food Court</th>
      <th>Airport Gate</th>
      <th>Airport Lounge</th>
      <th>Airport Service</th>
      <th>Airport Terminal</th>
      <th>...</th>
      <th>Trail</th>
      <th>Train Station</th>
      <th>Vegetarian / Vegan Restaurant</th>
      <th>Video Game Store</th>
      <th>Vietnamese Restaurant</th>
      <th>Wine Bar</th>
      <th>Wine Shop</th>
      <th>Wings Joint</th>
      <th>Women's Store</th>
      <th>Yoga Studio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
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
    </tr>
    <tr>
      <th>1</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
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
      <th>2</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
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
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
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
      <td>M4K</td>
      <td>East Toronto</td>
      <td>The Danforth West, Riverdale</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
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
<p>5 rows × 239 columns</p>
</div>



frequency ocurance for catagories


```python

toronto_central_venues_freq = toronto_central_onehot.groupby(['PostalCode', 'Borough', 'Neighborhoods']).mean().reset_index()
print(toronto_central_venues_freq.shape)
toronto_central_venues_freq.head()
```

    (39, 239)





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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhoods</th>
      <th>Afghan Restaurant</th>
      <th>Airport</th>
      <th>Airport Food Court</th>
      <th>Airport Gate</th>
      <th>Airport Lounge</th>
      <th>Airport Service</th>
      <th>Airport Terminal</th>
      <th>...</th>
      <th>Trail</th>
      <th>Train Station</th>
      <th>Vegetarian / Vegan Restaurant</th>
      <th>Video Game Store</th>
      <th>Vietnamese Restaurant</th>
      <th>Wine Bar</th>
      <th>Wine Shop</th>
      <th>Wings Joint</th>
      <th>Women's Store</th>
      <th>Yoga Studio</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.250000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M4K</td>
      <td>East Toronto</td>
      <td>The Danforth West, Riverdale</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.023256</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.023256</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M4L</td>
      <td>East Toronto</td>
      <td>India Bazaar, The Beaches West</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M4M</td>
      <td>East Toronto</td>
      <td>Studio District</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.025</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.025000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M4N</td>
      <td>Central Toronto</td>
      <td>Lawrence Park</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 239 columns</p>
</div>




```python

num_top_venues = 10

indicators = ['st', 'nd', 'rd']

# create columns according to number of top venues
areaColumns = ['PostalCode', 'Borough', 'Neighborhoods']
freqColumns = []
for ind in np.arange(num_top_venues):
    try:
        freqColumns.append('{}{} Most Common Venue'.format(ind+1, indicators[ind]))
    except:
        freqColumns.append('{}th Most Common Venue'.format(ind+1))
columns = areaColumns+freqColumns
# create a new dataframe
neighborhoods_venues_sorted = pd.DataFrame(columns=columns)
neighborhoods_venues_sorted['PostalCode'] = toronto_central_venues_freq['PostalCode']
neighborhoods_venues_sorted['Borough'] = toronto_central_venues_freq['Borough']
neighborhoods_venues_sorted['Neighborhoods'] = toronto_central_venues_freq['Neighborhoods']

for ind in np.arange(toronto_central_venues_freq.shape[0]):
    row_categories = toronto_central_venues_freq.iloc[ind, :].iloc[3:]
    row_categories_sorted = row_categories.sort_values(ascending=False)
    neighborhoods_venues_sorted.iloc[ind, 3:] = row_categories_sorted.index.values[0:num_top_venues]

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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhoods</th>
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
      <th>27</th>
      <td>M5V</td>
      <td>Downtown Toronto</td>
      <td>CN Tower, King and Spadina, Railway Lands, Har...</td>
      <td>Airport Service</td>
      <td>Airport Lounge</td>
      <td>Airport Terminal</td>
      <td>Harbor / Marina</td>
      <td>Plane</td>
      <td>Coffee Shop</td>
      <td>Sculpture Garden</td>
      <td>Boat or Ferry</td>
      <td>Rental Car Location</td>
      <td>Airport Gate</td>
    </tr>
    <tr>
      <th>31</th>
      <td>M6H</td>
      <td>West Toronto</td>
      <td>Dufferin, Dovercourt Village</td>
      <td>Bakery</td>
      <td>Pharmacy</td>
      <td>Brewery</td>
      <td>Supermarket</td>
      <td>Bar</td>
      <td>Bank</td>
      <td>Middle Eastern Restaurant</td>
      <td>Furniture / Home Store</td>
      <td>Music Venue</td>
      <td>Café</td>
    </tr>
    <tr>
      <th>32</th>
      <td>M6J</td>
      <td>West Toronto</td>
      <td>Little Portugal, Trinity</td>
      <td>Bar</td>
      <td>Asian Restaurant</td>
      <td>Men's Store</td>
      <td>Café</td>
      <td>Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
      <td>Coffee Shop</td>
      <td>Miscellaneous Shop</td>
      <td>Record Shop</td>
      <td>Cocktail Bar</td>
    </tr>
    <tr>
      <th>35</th>
      <td>M6R</td>
      <td>West Toronto</td>
      <td>Parkdale, Roncesvalles</td>
      <td>Breakfast Spot</td>
      <td>Gift Shop</td>
      <td>Bookstore</td>
      <td>Coffee Shop</td>
      <td>Movie Theater</td>
      <td>Italian Restaurant</td>
      <td>Restaurant</td>
      <td>Dessert Shop</td>
      <td>Dog Run</td>
      <td>Eastern European Restaurant</td>
    </tr>
    <tr>
      <th>25</th>
      <td>M5S</td>
      <td>Downtown Toronto</td>
      <td>University of Toronto, Harbord</td>
      <td>Café</td>
      <td>Bookstore</td>
      <td>Bar</td>
      <td>Italian Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Restaurant</td>
      <td>Bakery</td>
      <td>Yoga Studio</td>
      <td>Bank</td>
      <td>Beer Bar</td>
    </tr>
    <tr>
      <th>3</th>
      <td>M4M</td>
      <td>East Toronto</td>
      <td>Studio District</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Brewery</td>
      <td>Gastropub</td>
      <td>Bakery</td>
      <td>American Restaurant</td>
      <td>Yoga Studio</td>
      <td>Convenience Store</td>
      <td>Seafood Restaurant</td>
      <td>Sandwich Place</td>
    </tr>
    <tr>
      <th>15</th>
      <td>M5C</td>
      <td>Downtown Toronto</td>
      <td>St. James Town</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Cocktail Bar</td>
      <td>American Restaurant</td>
      <td>Restaurant</td>
      <td>Gastropub</td>
      <td>Art Gallery</td>
      <td>Cosmetics Shop</td>
      <td>Creperie</td>
      <td>Italian Restaurant</td>
    </tr>
    <tr>
      <th>26</th>
      <td>M5T</td>
      <td>Downtown Toronto</td>
      <td>Kensington Market, Chinatown, Grange Park</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Dessert Shop</td>
      <td>Vietnamese Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
      <td>Mexican Restaurant</td>
      <td>Pizza Place</td>
      <td>Bakery</td>
      <td>Park</td>
      <td>Bar</td>
    </tr>
    <tr>
      <th>34</th>
      <td>M6P</td>
      <td>West Toronto</td>
      <td>High Park, The Junction South</td>
      <td>Café</td>
      <td>Mexican Restaurant</td>
      <td>Thai Restaurant</td>
      <td>Bookstore</td>
      <td>Furniture / Home Store</td>
      <td>Liquor Store</td>
      <td>Fast Food Restaurant</td>
      <td>Cajun / Creole Restaurant</td>
      <td>Speakeasy</td>
      <td>Flea Market</td>
    </tr>
    <tr>
      <th>33</th>
      <td>M6K</td>
      <td>West Toronto</td>
      <td>Brockton, Parkdale Village, Exhibition Place</td>
      <td>Café</td>
      <td>Nightclub</td>
      <td>Coffee Shop</td>
      <td>Breakfast Spot</td>
      <td>Grocery Store</td>
      <td>Bakery</td>
      <td>Performing Arts Venue</td>
      <td>Pet Store</td>
      <td>Music Venue</td>
      <td>Climbing Gym</td>
    </tr>
    <tr>
      <th>11</th>
      <td>M4X</td>
      <td>Downtown Toronto</td>
      <td>St. James Town, Cabbagetown</td>
      <td>Café</td>
      <td>Pizza Place</td>
      <td>Restaurant</td>
      <td>Coffee Shop</td>
      <td>Bakery</td>
      <td>Pub</td>
      <td>Italian Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Indian Restaurant</td>
      <td>Plaza</td>
    </tr>
    <tr>
      <th>14</th>
      <td>M5B</td>
      <td>Downtown Toronto</td>
      <td>Garden District, Ryerson</td>
      <td>Clothing Store</td>
      <td>Coffee Shop</td>
      <td>Bubble Tea Shop</td>
      <td>Middle Eastern Restaurant</td>
      <td>Café</td>
      <td>Cosmetics Shop</td>
      <td>Italian Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Bookstore</td>
      <td>Tea Room</td>
    </tr>
    <tr>
      <th>6</th>
      <td>M4R</td>
      <td>Central Toronto</td>
      <td>North Toronto West, Lawrence Park</td>
      <td>Clothing Store</td>
      <td>Sporting Goods Shop</td>
      <td>Coffee Shop</td>
      <td>Yoga Studio</td>
      <td>Chinese Restaurant</td>
      <td>Spa</td>
      <td>Fast Food Restaurant</td>
      <td>Mexican Restaurant</td>
      <td>Café</td>
      <td>Salon / Barbershop</td>
    </tr>
    <tr>
      <th>19</th>
      <td>M5J</td>
      <td>Downtown Toronto</td>
      <td>Harbourfront East, Union Station, Toronto Islands</td>
      <td>Coffee Shop</td>
      <td>Aquarium</td>
      <td>Café</td>
      <td>Hotel</td>
      <td>Restaurant</td>
      <td>Italian Restaurant</td>
      <td>Sporting Goods Shop</td>
      <td>Brewery</td>
      <td>Scenic Lookout</td>
      <td>Fried Chicken Joint</td>
    </tr>
    <tr>
      <th>13</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Regent Park, Harbourfront</td>
      <td>Coffee Shop</td>
      <td>Bakery</td>
      <td>Pub</td>
      <td>Park</td>
      <td>Breakfast Spot</td>
      <td>Theater</td>
      <td>Café</td>
      <td>Chocolate Shop</td>
      <td>Distribution Center</td>
      <td>Restaurant</td>
    </tr>
    <tr>
      <th>29</th>
      <td>M5X</td>
      <td>Downtown Toronto</td>
      <td>First Canadian Place, Underground city</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Hotel</td>
      <td>Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Gym</td>
      <td>Seafood Restaurant</td>
      <td>Deli / Bodega</td>
      <td>Salad Place</td>
      <td>Steakhouse</td>
    </tr>
    <tr>
      <th>28</th>
      <td>M5W</td>
      <td>Downtown Toronto</td>
      <td>Stn A PO Boxes</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Italian Restaurant</td>
      <td>Seafood Restaurant</td>
      <td>Beer Bar</td>
      <td>Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Cocktail Bar</td>
      <td>Breakfast Spot</td>
      <td>Hotel</td>
    </tr>
    <tr>
      <th>18</th>
      <td>M5H</td>
      <td>Downtown Toronto</td>
      <td>Richmond, Adelaide, King</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Restaurant</td>
      <td>Hotel</td>
      <td>Deli / Bodega</td>
      <td>Gym</td>
      <td>Thai Restaurant</td>
      <td>Clothing Store</td>
      <td>Steakhouse</td>
      <td>Bookstore</td>
    </tr>
    <tr>
      <th>16</th>
      <td>M5E</td>
      <td>Downtown Toronto</td>
      <td>Berczy Park</td>
      <td>Coffee Shop</td>
      <td>Cocktail Bar</td>
      <td>Cheese Shop</td>
      <td>Café</td>
      <td>Restaurant</td>
      <td>Bakery</td>
      <td>Beer Bar</td>
      <td>Seafood Restaurant</td>
      <td>Park</td>
      <td>Clothing Store</td>
    </tr>
    <tr>
      <th>20</th>
      <td>M5K</td>
      <td>Downtown Toronto</td>
      <td>Toronto Dominion Centre, Design Exchange</td>
      <td>Coffee Shop</td>
      <td>Hotel</td>
      <td>Café</td>
      <td>Restaurant</td>
      <td>Italian Restaurant</td>
      <td>American Restaurant</td>
      <td>Seafood Restaurant</td>
      <td>Salad Place</td>
      <td>Deli / Bodega</td>
      <td>Japanese Restaurant</td>
    </tr>
    <tr>
      <th>17</th>
      <td>M5G</td>
      <td>Downtown Toronto</td>
      <td>Central Bay Street</td>
      <td>Coffee Shop</td>
      <td>Italian Restaurant</td>
      <td>Sandwich Place</td>
      <td>Japanese Restaurant</td>
      <td>Café</td>
      <td>Middle Eastern Restaurant</td>
      <td>Bubble Tea Shop</td>
      <td>Department Store</td>
      <td>Salad Place</td>
      <td>Burger Joint</td>
    </tr>
    <tr>
      <th>21</th>
      <td>M5L</td>
      <td>Downtown Toronto</td>
      <td>Commerce Court, Victoria Hotel</td>
      <td>Coffee Shop</td>
      <td>Restaurant</td>
      <td>Café</td>
      <td>Hotel</td>
      <td>Gym</td>
      <td>American Restaurant</td>
      <td>Deli / Bodega</td>
      <td>Seafood Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Italian Restaurant</td>
    </tr>
    <tr>
      <th>12</th>
      <td>M4Y</td>
      <td>Downtown Toronto</td>
      <td>Church and Wellesley</td>
      <td>Coffee Shop</td>
      <td>Sushi Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Restaurant</td>
      <td>Gay Bar</td>
      <td>Pub</td>
      <td>Men's Store</td>
      <td>Mediterranean Restaurant</td>
      <td>Hotel</td>
      <td>Dance Studio</td>
    </tr>
    <tr>
      <th>37</th>
      <td>M7A</td>
      <td>Downtown Toronto</td>
      <td>Queen's Park, Ontario Provincial Government</td>
      <td>Coffee Shop</td>
      <td>Sushi Restaurant</td>
      <td>Yoga Studio</td>
      <td>Arts &amp; Crafts Store</td>
      <td>Sandwich Place</td>
      <td>Café</td>
      <td>Smoothie Shop</td>
      <td>Beer Bar</td>
      <td>Italian Restaurant</td>
      <td>Mexican Restaurant</td>
    </tr>
    <tr>
      <th>7</th>
      <td>M4S</td>
      <td>Central Toronto</td>
      <td>Davisville</td>
      <td>Dessert Shop</td>
      <td>Sandwich Place</td>
      <td>Pizza Place</td>
      <td>Italian Restaurant</td>
      <td>Gym</td>
      <td>Sushi Restaurant</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Pharmacy</td>
      <td>Diner</td>
    </tr>
    <tr>
      <th>2</th>
      <td>M4L</td>
      <td>East Toronto</td>
      <td>India Bazaar, The Beaches West</td>
      <td>Fast Food Restaurant</td>
      <td>Pet Store</td>
      <td>Pub</td>
      <td>Brewery</td>
      <td>Burrito Place</td>
      <td>Sandwich Place</td>
      <td>Fish &amp; Chips Shop</td>
      <td>Steakhouse</td>
      <td>Italian Restaurant</td>
      <td>Sushi Restaurant</td>
    </tr>
    <tr>
      <th>22</th>
      <td>M5N</td>
      <td>Central Toronto</td>
      <td>Roselawn</td>
      <td>Garden</td>
      <td>Yoga Studio</td>
      <td>Fish &amp; Chips Shop</td>
      <td>Fast Food Restaurant</td>
      <td>Farmers Market</td>
      <td>Falafel Restaurant</td>
      <td>Event Space</td>
      <td>Ethiopian Restaurant</td>
      <td>Electronics Store</td>
      <td>Eastern European Restaurant</td>
    </tr>
    <tr>
      <th>1</th>
      <td>M4K</td>
      <td>East Toronto</td>
      <td>The Danforth West, Riverdale</td>
      <td>Greek Restaurant</td>
      <td>Coffee Shop</td>
      <td>Italian Restaurant</td>
      <td>Bookstore</td>
      <td>Ice Cream Shop</td>
      <td>Furniture / Home Store</td>
      <td>Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Pub</td>
      <td>Juice Bar</td>
    </tr>
    <tr>
      <th>30</th>
      <td>M6G</td>
      <td>Downtown Toronto</td>
      <td>Christie</td>
      <td>Grocery Store</td>
      <td>Café</td>
      <td>Park</td>
      <td>Coffee Shop</td>
      <td>Candy Store</td>
      <td>Italian Restaurant</td>
      <td>Baby Store</td>
      <td>Restaurant</td>
      <td>Nightclub</td>
      <td>Diner</td>
    </tr>
    <tr>
      <th>0</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>Neighborhood</td>
      <td>Trail</td>
      <td>Health Food Store</td>
      <td>Pub</td>
      <td>Discount Store</td>
      <td>Distribution Center</td>
      <td>Dog Run</td>
      <td>Doner Restaurant</td>
      <td>Donut Shop</td>
      <td>Dumpling Restaurant</td>
    </tr>
    <tr>
      <th>10</th>
      <td>M4W</td>
      <td>Downtown Toronto</td>
      <td>Rosedale</td>
      <td>Park</td>
      <td>Playground</td>
      <td>Trail</td>
      <td>Yoga Studio</td>
      <td>Diner</td>
      <td>Falafel Restaurant</td>
      <td>Event Space</td>
      <td>Ethiopian Restaurant</td>
      <td>Electronics Store</td>
      <td>Eastern European Restaurant</td>
    </tr>
    <tr>
      <th>4</th>
      <td>M4N</td>
      <td>Central Toronto</td>
      <td>Lawrence Park</td>
      <td>Park</td>
      <td>Swim School</td>
      <td>Bus Line</td>
      <td>Yoga Studio</td>
      <td>Distribution Center</td>
      <td>Farmers Market</td>
      <td>Falafel Restaurant</td>
      <td>Event Space</td>
      <td>Ethiopian Restaurant</td>
      <td>Electronics Store</td>
    </tr>
    <tr>
      <th>5</th>
      <td>M4P</td>
      <td>Central Toronto</td>
      <td>Davisville North</td>
      <td>Pizza Place</td>
      <td>Hotel</td>
      <td>Park</td>
      <td>Department Store</td>
      <td>Sandwich Place</td>
      <td>Breakfast Spot</td>
      <td>Food &amp; Drink Shop</td>
      <td>Gym / Fitness Center</td>
      <td>General Travel</td>
      <td>Event Space</td>
    </tr>
    <tr>
      <th>9</th>
      <td>M4V</td>
      <td>Central Toronto</td>
      <td>Summerhill West, Rathnelly, South Hill, Forest...</td>
      <td>Pub</td>
      <td>Coffee Shop</td>
      <td>Fried Chicken Joint</td>
      <td>Sports Bar</td>
      <td>Restaurant</td>
      <td>Supermarket</td>
      <td>Sushi Restaurant</td>
      <td>Bank</td>
      <td>Bagel Shop</td>
      <td>Liquor Store</td>
    </tr>
    <tr>
      <th>24</th>
      <td>M5R</td>
      <td>Central Toronto</td>
      <td>The Annex, North Midtown, Yorkville</td>
      <td>Sandwich Place</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Pharmacy</td>
      <td>History Museum</td>
      <td>Middle Eastern Restaurant</td>
      <td>Indian Restaurant</td>
      <td>BBQ Joint</td>
      <td>Pub</td>
      <td>Donut Shop</td>
    </tr>
    <tr>
      <th>8</th>
      <td>M4T</td>
      <td>Central Toronto</td>
      <td>Moore Park, Summerhill East</td>
      <td>Summer Camp</td>
      <td>Trail</td>
      <td>Lawyer</td>
      <td>Tennis Court</td>
      <td>Dog Run</td>
      <td>Doner Restaurant</td>
      <td>Donut Shop</td>
      <td>Dumpling Restaurant</td>
      <td>Eastern European Restaurant</td>
      <td>Yoga Studio</td>
    </tr>
    <tr>
      <th>36</th>
      <td>M6S</td>
      <td>West Toronto</td>
      <td>Runnymede, Swansea</td>
      <td>Sushi Restaurant</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Italian Restaurant</td>
      <td>Pub</td>
      <td>Pizza Place</td>
      <td>Bar</td>
      <td>Bookstore</td>
      <td>Smoothie Shop</td>
      <td>Burrito Place</td>
    </tr>
    <tr>
      <th>23</th>
      <td>M5P</td>
      <td>Central Toronto</td>
      <td>Forest Hill North &amp; West, Forest Hill Road Park</td>
      <td>Trail</td>
      <td>Park</td>
      <td>Sushi Restaurant</td>
      <td>Jewelry Store</td>
      <td>Yoga Studio</td>
      <td>Dog Run</td>
      <td>Doner Restaurant</td>
      <td>Donut Shop</td>
      <td>Dumpling Restaurant</td>
      <td>Eastern European Restaurant</td>
    </tr>
    <tr>
      <th>38</th>
      <td>M7Y</td>
      <td>East Toronto</td>
      <td>Business reply mail Processing Centre, South C...</td>
      <td>Yoga Studio</td>
      <td>Auto Workshop</td>
      <td>Garden Center</td>
      <td>Garden</td>
      <td>Light Rail Station</td>
      <td>Fast Food Restaurant</td>
      <td>Farmers Market</td>
      <td>Comic Shop</td>
      <td>Park</td>
      <td>Restaurant</td>
    </tr>
  </tbody>
</table>
</div>




```python
kclusters = 3

toronto_central_venues_freq_clustering = toronto_central_venues_freq.drop(['PostalCode', 'Borough', 'Neighborhoods'], 1)

kmeans = KMeans(n_clusters=kclusters, random_state=0).fit(toronto_central_venues_freq_clustering)

toronto_central_clustered_df = df4
toronto_central_clustered_df['Cluster'] = kmeans.labels_

toronto_central_clustered_df = toronto_central_clustered_df.join(neighborhoods_venues_sorted.drop(['Borough', 'Neighborhoods'], 1).set_index('PostalCode'), on='PostalCode')
toronto_central_clustered_df.sort_values(['Cluster'] + freqColumns, inplace=True)
toronto_central_clustered_df
```

    /home/jupyterlab/conda/envs/python/lib/python3.6/site-packages/ipykernel_launcher.py:8: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      





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
      <th>PostalCode</th>
      <th>Borough</th>
      <th>Neighborhood</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Cluster</th>
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
      <th>68</th>
      <td>M5V</td>
      <td>Downtown Toronto</td>
      <td>CN Tower, King and Spadina, Railway Lands, Har...</td>
      <td>43.628947</td>
      <td>-79.394420</td>
      <td>0</td>
      <td>Airport Service</td>
      <td>Airport Lounge</td>
      <td>Airport Terminal</td>
      <td>Harbor / Marina</td>
      <td>Plane</td>
      <td>Coffee Shop</td>
      <td>Sculpture Garden</td>
      <td>Boat or Ferry</td>
      <td>Rental Car Location</td>
      <td>Airport Gate</td>
    </tr>
    <tr>
      <th>76</th>
      <td>M6H</td>
      <td>West Toronto</td>
      <td>Dufferin, Dovercourt Village</td>
      <td>43.669005</td>
      <td>-79.442259</td>
      <td>0</td>
      <td>Bakery</td>
      <td>Pharmacy</td>
      <td>Brewery</td>
      <td>Supermarket</td>
      <td>Bar</td>
      <td>Bank</td>
      <td>Middle Eastern Restaurant</td>
      <td>Furniture / Home Store</td>
      <td>Music Venue</td>
      <td>Café</td>
    </tr>
    <tr>
      <th>77</th>
      <td>M6J</td>
      <td>West Toronto</td>
      <td>Little Portugal, Trinity</td>
      <td>43.647927</td>
      <td>-79.419750</td>
      <td>0</td>
      <td>Bar</td>
      <td>Asian Restaurant</td>
      <td>Men's Store</td>
      <td>Café</td>
      <td>Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
      <td>Coffee Shop</td>
      <td>Miscellaneous Shop</td>
      <td>Record Shop</td>
      <td>Cocktail Bar</td>
    </tr>
    <tr>
      <th>83</th>
      <td>M6R</td>
      <td>West Toronto</td>
      <td>Parkdale, Roncesvalles</td>
      <td>43.648960</td>
      <td>-79.456325</td>
      <td>0</td>
      <td>Breakfast Spot</td>
      <td>Gift Shop</td>
      <td>Bookstore</td>
      <td>Coffee Shop</td>
      <td>Movie Theater</td>
      <td>Italian Restaurant</td>
      <td>Restaurant</td>
      <td>Dessert Shop</td>
      <td>Dog Run</td>
      <td>Eastern European Restaurant</td>
    </tr>
    <tr>
      <th>66</th>
      <td>M5S</td>
      <td>Downtown Toronto</td>
      <td>University of Toronto, Harbord</td>
      <td>43.662696</td>
      <td>-79.400049</td>
      <td>0</td>
      <td>Café</td>
      <td>Bookstore</td>
      <td>Bar</td>
      <td>Italian Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Restaurant</td>
      <td>Bakery</td>
      <td>Yoga Studio</td>
      <td>Bank</td>
      <td>Beer Bar</td>
    </tr>
    <tr>
      <th>43</th>
      <td>M4M</td>
      <td>East Toronto</td>
      <td>Studio District</td>
      <td>43.659526</td>
      <td>-79.340923</td>
      <td>0</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Brewery</td>
      <td>Gastropub</td>
      <td>Bakery</td>
      <td>American Restaurant</td>
      <td>Yoga Studio</td>
      <td>Convenience Store</td>
      <td>Seafood Restaurant</td>
      <td>Sandwich Place</td>
    </tr>
    <tr>
      <th>55</th>
      <td>M5C</td>
      <td>Downtown Toronto</td>
      <td>St. James Town</td>
      <td>43.651494</td>
      <td>-79.375418</td>
      <td>0</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Cocktail Bar</td>
      <td>American Restaurant</td>
      <td>Restaurant</td>
      <td>Gastropub</td>
      <td>Art Gallery</td>
      <td>Cosmetics Shop</td>
      <td>Creperie</td>
      <td>Italian Restaurant</td>
    </tr>
    <tr>
      <th>67</th>
      <td>M5T</td>
      <td>Downtown Toronto</td>
      <td>Kensington Market, Chinatown, Grange Park</td>
      <td>43.653206</td>
      <td>-79.400049</td>
      <td>0</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Dessert Shop</td>
      <td>Vietnamese Restaurant</td>
      <td>Vegetarian / Vegan Restaurant</td>
      <td>Mexican Restaurant</td>
      <td>Pizza Place</td>
      <td>Bakery</td>
      <td>Park</td>
      <td>Bar</td>
    </tr>
    <tr>
      <th>82</th>
      <td>M6P</td>
      <td>West Toronto</td>
      <td>High Park, The Junction South</td>
      <td>43.661608</td>
      <td>-79.464763</td>
      <td>0</td>
      <td>Café</td>
      <td>Mexican Restaurant</td>
      <td>Thai Restaurant</td>
      <td>Bookstore</td>
      <td>Furniture / Home Store</td>
      <td>Liquor Store</td>
      <td>Fast Food Restaurant</td>
      <td>Cajun / Creole Restaurant</td>
      <td>Speakeasy</td>
      <td>Flea Market</td>
    </tr>
    <tr>
      <th>78</th>
      <td>M6K</td>
      <td>West Toronto</td>
      <td>Brockton, Parkdale Village, Exhibition Place</td>
      <td>43.636847</td>
      <td>-79.428191</td>
      <td>0</td>
      <td>Café</td>
      <td>Nightclub</td>
      <td>Coffee Shop</td>
      <td>Breakfast Spot</td>
      <td>Grocery Store</td>
      <td>Bakery</td>
      <td>Performing Arts Venue</td>
      <td>Pet Store</td>
      <td>Music Venue</td>
      <td>Climbing Gym</td>
    </tr>
    <tr>
      <th>51</th>
      <td>M4X</td>
      <td>Downtown Toronto</td>
      <td>St. James Town, Cabbagetown</td>
      <td>43.667967</td>
      <td>-79.367675</td>
      <td>0</td>
      <td>Café</td>
      <td>Pizza Place</td>
      <td>Restaurant</td>
      <td>Coffee Shop</td>
      <td>Bakery</td>
      <td>Pub</td>
      <td>Italian Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Indian Restaurant</td>
      <td>Plaza</td>
    </tr>
    <tr>
      <th>54</th>
      <td>M5B</td>
      <td>Downtown Toronto</td>
      <td>Garden District, Ryerson</td>
      <td>43.657162</td>
      <td>-79.378937</td>
      <td>0</td>
      <td>Clothing Store</td>
      <td>Coffee Shop</td>
      <td>Bubble Tea Shop</td>
      <td>Middle Eastern Restaurant</td>
      <td>Café</td>
      <td>Cosmetics Shop</td>
      <td>Italian Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Bookstore</td>
      <td>Tea Room</td>
    </tr>
    <tr>
      <th>46</th>
      <td>M4R</td>
      <td>Central Toronto</td>
      <td>North Toronto West, Lawrence Park</td>
      <td>43.715383</td>
      <td>-79.405678</td>
      <td>0</td>
      <td>Clothing Store</td>
      <td>Sporting Goods Shop</td>
      <td>Coffee Shop</td>
      <td>Yoga Studio</td>
      <td>Chinese Restaurant</td>
      <td>Spa</td>
      <td>Fast Food Restaurant</td>
      <td>Mexican Restaurant</td>
      <td>Café</td>
      <td>Salon / Barbershop</td>
    </tr>
    <tr>
      <th>59</th>
      <td>M5J</td>
      <td>Downtown Toronto</td>
      <td>Harbourfront East, Union Station, Toronto Islands</td>
      <td>43.640816</td>
      <td>-79.381752</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Aquarium</td>
      <td>Café</td>
      <td>Hotel</td>
      <td>Restaurant</td>
      <td>Italian Restaurant</td>
      <td>Sporting Goods Shop</td>
      <td>Brewery</td>
      <td>Scenic Lookout</td>
      <td>Fried Chicken Joint</td>
    </tr>
    <tr>
      <th>53</th>
      <td>M5A</td>
      <td>Downtown Toronto</td>
      <td>Regent Park, Harbourfront</td>
      <td>43.654260</td>
      <td>-79.360636</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Bakery</td>
      <td>Pub</td>
      <td>Park</td>
      <td>Breakfast Spot</td>
      <td>Theater</td>
      <td>Café</td>
      <td>Chocolate Shop</td>
      <td>Distribution Center</td>
      <td>Restaurant</td>
    </tr>
    <tr>
      <th>70</th>
      <td>M5X</td>
      <td>Downtown Toronto</td>
      <td>First Canadian Place, Underground city</td>
      <td>43.648429</td>
      <td>-79.382280</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Hotel</td>
      <td>Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Gym</td>
      <td>Seafood Restaurant</td>
      <td>Deli / Bodega</td>
      <td>Salad Place</td>
      <td>Steakhouse</td>
    </tr>
    <tr>
      <th>69</th>
      <td>M5W</td>
      <td>Downtown Toronto</td>
      <td>Stn A PO Boxes</td>
      <td>43.646435</td>
      <td>-79.374846</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Italian Restaurant</td>
      <td>Seafood Restaurant</td>
      <td>Beer Bar</td>
      <td>Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Cocktail Bar</td>
      <td>Breakfast Spot</td>
      <td>Hotel</td>
    </tr>
    <tr>
      <th>58</th>
      <td>M5H</td>
      <td>Downtown Toronto</td>
      <td>Richmond, Adelaide, King</td>
      <td>43.650571</td>
      <td>-79.384568</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Restaurant</td>
      <td>Hotel</td>
      <td>Deli / Bodega</td>
      <td>Gym</td>
      <td>Thai Restaurant</td>
      <td>Clothing Store</td>
      <td>Steakhouse</td>
      <td>Bookstore</td>
    </tr>
    <tr>
      <th>56</th>
      <td>M5E</td>
      <td>Downtown Toronto</td>
      <td>Berczy Park</td>
      <td>43.644771</td>
      <td>-79.373306</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Cocktail Bar</td>
      <td>Cheese Shop</td>
      <td>Café</td>
      <td>Restaurant</td>
      <td>Bakery</td>
      <td>Beer Bar</td>
      <td>Seafood Restaurant</td>
      <td>Park</td>
      <td>Clothing Store</td>
    </tr>
    <tr>
      <th>60</th>
      <td>M5K</td>
      <td>Downtown Toronto</td>
      <td>Toronto Dominion Centre, Design Exchange</td>
      <td>43.647177</td>
      <td>-79.381576</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Hotel</td>
      <td>Café</td>
      <td>Restaurant</td>
      <td>Italian Restaurant</td>
      <td>American Restaurant</td>
      <td>Seafood Restaurant</td>
      <td>Salad Place</td>
      <td>Deli / Bodega</td>
      <td>Japanese Restaurant</td>
    </tr>
    <tr>
      <th>57</th>
      <td>M5G</td>
      <td>Downtown Toronto</td>
      <td>Central Bay Street</td>
      <td>43.657952</td>
      <td>-79.387383</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Italian Restaurant</td>
      <td>Sandwich Place</td>
      <td>Japanese Restaurant</td>
      <td>Café</td>
      <td>Middle Eastern Restaurant</td>
      <td>Bubble Tea Shop</td>
      <td>Department Store</td>
      <td>Salad Place</td>
      <td>Burger Joint</td>
    </tr>
    <tr>
      <th>61</th>
      <td>M5L</td>
      <td>Downtown Toronto</td>
      <td>Commerce Court, Victoria Hotel</td>
      <td>43.648198</td>
      <td>-79.379817</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Restaurant</td>
      <td>Café</td>
      <td>Hotel</td>
      <td>Gym</td>
      <td>American Restaurant</td>
      <td>Deli / Bodega</td>
      <td>Seafood Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Italian Restaurant</td>
    </tr>
    <tr>
      <th>52</th>
      <td>M4Y</td>
      <td>Downtown Toronto</td>
      <td>Church and Wellesley</td>
      <td>43.665860</td>
      <td>-79.383160</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Sushi Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Restaurant</td>
      <td>Gay Bar</td>
      <td>Pub</td>
      <td>Men's Store</td>
      <td>Mediterranean Restaurant</td>
      <td>Hotel</td>
      <td>Dance Studio</td>
    </tr>
    <tr>
      <th>85</th>
      <td>M7A</td>
      <td>Downtown Toronto</td>
      <td>Queen's Park, Ontario Provincial Government</td>
      <td>43.662301</td>
      <td>-79.389494</td>
      <td>0</td>
      <td>Coffee Shop</td>
      <td>Sushi Restaurant</td>
      <td>Yoga Studio</td>
      <td>Arts &amp; Crafts Store</td>
      <td>Sandwich Place</td>
      <td>Café</td>
      <td>Smoothie Shop</td>
      <td>Beer Bar</td>
      <td>Italian Restaurant</td>
      <td>Mexican Restaurant</td>
    </tr>
    <tr>
      <th>47</th>
      <td>M4S</td>
      <td>Central Toronto</td>
      <td>Davisville</td>
      <td>43.704324</td>
      <td>-79.388790</td>
      <td>0</td>
      <td>Dessert Shop</td>
      <td>Sandwich Place</td>
      <td>Pizza Place</td>
      <td>Italian Restaurant</td>
      <td>Gym</td>
      <td>Sushi Restaurant</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Pharmacy</td>
      <td>Diner</td>
    </tr>
    <tr>
      <th>42</th>
      <td>M4L</td>
      <td>East Toronto</td>
      <td>India Bazaar, The Beaches West</td>
      <td>43.668999</td>
      <td>-79.315572</td>
      <td>0</td>
      <td>Fast Food Restaurant</td>
      <td>Pet Store</td>
      <td>Pub</td>
      <td>Brewery</td>
      <td>Burrito Place</td>
      <td>Sandwich Place</td>
      <td>Fish &amp; Chips Shop</td>
      <td>Steakhouse</td>
      <td>Italian Restaurant</td>
      <td>Sushi Restaurant</td>
    </tr>
    <tr>
      <th>41</th>
      <td>M4K</td>
      <td>East Toronto</td>
      <td>The Danforth West, Riverdale</td>
      <td>43.679557</td>
      <td>-79.352188</td>
      <td>0</td>
      <td>Greek Restaurant</td>
      <td>Coffee Shop</td>
      <td>Italian Restaurant</td>
      <td>Bookstore</td>
      <td>Ice Cream Shop</td>
      <td>Furniture / Home Store</td>
      <td>Restaurant</td>
      <td>Japanese Restaurant</td>
      <td>Pub</td>
      <td>Juice Bar</td>
    </tr>
    <tr>
      <th>75</th>
      <td>M6G</td>
      <td>Downtown Toronto</td>
      <td>Christie</td>
      <td>43.669542</td>
      <td>-79.422564</td>
      <td>0</td>
      <td>Grocery Store</td>
      <td>Café</td>
      <td>Park</td>
      <td>Coffee Shop</td>
      <td>Candy Store</td>
      <td>Italian Restaurant</td>
      <td>Baby Store</td>
      <td>Restaurant</td>
      <td>Nightclub</td>
      <td>Diner</td>
    </tr>
    <tr>
      <th>37</th>
      <td>M4E</td>
      <td>East Toronto</td>
      <td>The Beaches</td>
      <td>43.676357</td>
      <td>-79.293031</td>
      <td>0</td>
      <td>Neighborhood</td>
      <td>Trail</td>
      <td>Health Food Store</td>
      <td>Pub</td>
      <td>Discount Store</td>
      <td>Distribution Center</td>
      <td>Dog Run</td>
      <td>Doner Restaurant</td>
      <td>Donut Shop</td>
      <td>Dumpling Restaurant</td>
    </tr>
    <tr>
      <th>44</th>
      <td>M4N</td>
      <td>Central Toronto</td>
      <td>Lawrence Park</td>
      <td>43.728020</td>
      <td>-79.388790</td>
      <td>0</td>
      <td>Park</td>
      <td>Swim School</td>
      <td>Bus Line</td>
      <td>Yoga Studio</td>
      <td>Distribution Center</td>
      <td>Farmers Market</td>
      <td>Falafel Restaurant</td>
      <td>Event Space</td>
      <td>Ethiopian Restaurant</td>
      <td>Electronics Store</td>
    </tr>
    <tr>
      <th>45</th>
      <td>M4P</td>
      <td>Central Toronto</td>
      <td>Davisville North</td>
      <td>43.712751</td>
      <td>-79.390197</td>
      <td>0</td>
      <td>Pizza Place</td>
      <td>Hotel</td>
      <td>Park</td>
      <td>Department Store</td>
      <td>Sandwich Place</td>
      <td>Breakfast Spot</td>
      <td>Food &amp; Drink Shop</td>
      <td>Gym / Fitness Center</td>
      <td>General Travel</td>
      <td>Event Space</td>
    </tr>
    <tr>
      <th>49</th>
      <td>M4V</td>
      <td>Central Toronto</td>
      <td>Summerhill West, Rathnelly, South Hill, Forest...</td>
      <td>43.686412</td>
      <td>-79.400049</td>
      <td>0</td>
      <td>Pub</td>
      <td>Coffee Shop</td>
      <td>Fried Chicken Joint</td>
      <td>Sports Bar</td>
      <td>Restaurant</td>
      <td>Supermarket</td>
      <td>Sushi Restaurant</td>
      <td>Bank</td>
      <td>Bagel Shop</td>
      <td>Liquor Store</td>
    </tr>
    <tr>
      <th>65</th>
      <td>M5R</td>
      <td>Central Toronto</td>
      <td>The Annex, North Midtown, Yorkville</td>
      <td>43.672710</td>
      <td>-79.405678</td>
      <td>0</td>
      <td>Sandwich Place</td>
      <td>Café</td>
      <td>Coffee Shop</td>
      <td>Pharmacy</td>
      <td>History Museum</td>
      <td>Middle Eastern Restaurant</td>
      <td>Indian Restaurant</td>
      <td>BBQ Joint</td>
      <td>Pub</td>
      <td>Donut Shop</td>
    </tr>
    <tr>
      <th>48</th>
      <td>M4T</td>
      <td>Central Toronto</td>
      <td>Moore Park, Summerhill East</td>
      <td>43.689574</td>
      <td>-79.383160</td>
      <td>0</td>
      <td>Summer Camp</td>
      <td>Trail</td>
      <td>Lawyer</td>
      <td>Tennis Court</td>
      <td>Dog Run</td>
      <td>Doner Restaurant</td>
      <td>Donut Shop</td>
      <td>Dumpling Restaurant</td>
      <td>Eastern European Restaurant</td>
      <td>Yoga Studio</td>
    </tr>
    <tr>
      <th>84</th>
      <td>M6S</td>
      <td>West Toronto</td>
      <td>Runnymede, Swansea</td>
      <td>43.651571</td>
      <td>-79.484450</td>
      <td>0</td>
      <td>Sushi Restaurant</td>
      <td>Coffee Shop</td>
      <td>Café</td>
      <td>Italian Restaurant</td>
      <td>Pub</td>
      <td>Pizza Place</td>
      <td>Bar</td>
      <td>Bookstore</td>
      <td>Smoothie Shop</td>
      <td>Burrito Place</td>
    </tr>
    <tr>
      <th>87</th>
      <td>M7Y</td>
      <td>East Toronto</td>
      <td>Business reply mail Processing Centre, South C...</td>
      <td>43.662744</td>
      <td>-79.321558</td>
      <td>0</td>
      <td>Yoga Studio</td>
      <td>Auto Workshop</td>
      <td>Garden Center</td>
      <td>Garden</td>
      <td>Light Rail Station</td>
      <td>Fast Food Restaurant</td>
      <td>Farmers Market</td>
      <td>Comic Shop</td>
      <td>Park</td>
      <td>Restaurant</td>
    </tr>
    <tr>
      <th>63</th>
      <td>M5N</td>
      <td>Central Toronto</td>
      <td>Roselawn</td>
      <td>43.711695</td>
      <td>-79.416936</td>
      <td>1</td>
      <td>Garden</td>
      <td>Yoga Studio</td>
      <td>Fish &amp; Chips Shop</td>
      <td>Fast Food Restaurant</td>
      <td>Farmers Market</td>
      <td>Falafel Restaurant</td>
      <td>Event Space</td>
      <td>Ethiopian Restaurant</td>
      <td>Electronics Store</td>
      <td>Eastern European Restaurant</td>
    </tr>
    <tr>
      <th>50</th>
      <td>M4W</td>
      <td>Downtown Toronto</td>
      <td>Rosedale</td>
      <td>43.679563</td>
      <td>-79.377529</td>
      <td>2</td>
      <td>Park</td>
      <td>Playground</td>
      <td>Trail</td>
      <td>Yoga Studio</td>
      <td>Diner</td>
      <td>Falafel Restaurant</td>
      <td>Event Space</td>
      <td>Ethiopian Restaurant</td>
      <td>Electronics Store</td>
      <td>Eastern European Restaurant</td>
    </tr>
    <tr>
      <th>64</th>
      <td>M5P</td>
      <td>Central Toronto</td>
      <td>Forest Hill North &amp; West, Forest Hill Road Park</td>
      <td>43.696948</td>
      <td>-79.411307</td>
      <td>2</td>
      <td>Trail</td>
      <td>Park</td>
      <td>Sushi Restaurant</td>
      <td>Jewelry Store</td>
      <td>Yoga Studio</td>
      <td>Dog Run</td>
      <td>Doner Restaurant</td>
      <td>Donut Shop</td>
      <td>Dumpling Restaurant</td>
      <td>Eastern European Restaurant</td>
    </tr>
  </tbody>
</table>
</div>




```python
latitude = 43.657952
longitude = -79.387383
map_clusters = folium.Map(location=[latitude, longitude], zoom_start=11)

# set color scheme for the clusters
x = np.arange(kclusters)
ys = [i + x + (i*x)**2 for i in range(kclusters)]
colors_array = cm.rainbow(np.linspace(0, 1, len(ys)))
rainbow = [colors.rgb2hex(i) for i in colors_array]

map_clusters
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe src="about:blank" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" data-html=PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVMgPSBmYWxzZTsgTF9OT19UT1VDSCA9IGZhbHNlOyBMX0RJU0FCTEVfM0QgPSBmYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC10aGVtZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9yYXdnaXQuY29tL3B5dGhvbi12aXN1YWxpemF0aW9uL2ZvbGl1bS9tYXN0ZXIvZm9saXVtL3RlbXBsYXRlcy9sZWFmbGV0LmF3ZXNvbWUucm90YXRlLmNzcyIvPgogICAgPHN0eWxlPmh0bWwsIGJvZHkge3dpZHRoOiAxMDAlO2hlaWdodDogMTAwJTttYXJnaW46IDA7cGFkZGluZzogMDt9PC9zdHlsZT4KICAgIDxzdHlsZT4jbWFwIHtwb3NpdGlvbjphYnNvbHV0ZTt0b3A6MDtib3R0b206MDtyaWdodDowO2xlZnQ6MDt9PC9zdHlsZT4KICAgIAogICAgICAgICAgICA8c3R5bGU+ICNtYXBfZWI2YjBjOTBmMmI5NDkwNzgzYmZhNDk1ZjcwZGRiMzkgewogICAgICAgICAgICAgICAgcG9zaXRpb24gOiByZWxhdGl2ZTsKICAgICAgICAgICAgICAgIHdpZHRoIDogMTAwLjAlOwogICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgICAgICAgICAgdG9wOiAwLjAlOwogICAgICAgICAgICAgICAgfQogICAgICAgICAgICA8L3N0eWxlPgogICAgICAgIAo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgICAgICAgICA8ZGl2IGNsYXNzPSJmb2xpdW0tbWFwIiBpZD0ibWFwX2ViNmIwYzkwZjJiOTQ5MDc4M2JmYTQ5NWY3MGRkYjM5IiA+PC9kaXY+CiAgICAgICAgCjwvYm9keT4KPHNjcmlwdD4gICAgCiAgICAKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGJvdW5kcyA9IG51bGw7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcF9lYjZiMGM5MGYyYjk0OTA3ODNiZmE0OTVmNzBkZGIzOSA9IEwubWFwKAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgJ21hcF9lYjZiMGM5MGYyYjk0OTA3ODNiZmE0OTVmNzBkZGIzOScsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB7Y2VudGVyOiBbNDMuNjU3OTUyLC03OS4zODczODNdLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgem9vbTogMTEsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBtYXhCb3VuZHM6IGJvdW5kcywKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGxheWVyczogW10sCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB3b3JsZENvcHlKdW1wOiBmYWxzZSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIGNyczogTC5DUlMuRVBTRzM4NTcKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgfSk7CiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciB0aWxlX2xheWVyXzk5YzI4OWQwYzJjNjRiM2ZhNGM1M2Q4YmJhYTgyOTZhID0gTC50aWxlTGF5ZXIoCiAgICAgICAgICAgICAgICAnaHR0cHM6Ly97c30udGlsZS5vcGVuc3RyZWV0bWFwLm9yZy97en0ve3h9L3t5fS5wbmcnLAogICAgICAgICAgICAgICAgewogICJhdHRyaWJ1dGlvbiI6IG51bGwsCiAgImRldGVjdFJldGluYSI6IGZhbHNlLAogICJtYXhab29tIjogMTgsCiAgIm1pblpvb20iOiAxLAogICJub1dyYXAiOiBmYWxzZSwKICAic3ViZG9tYWlucyI6ICJhYmMiCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwX2ViNmIwYzkwZjJiOTQ5MDc4M2JmYTQ5NWY3MGRkYjM5KTsKICAgICAgICAKPC9zY3JpcHQ+ onload="this.contentDocument.open();this.contentDocument.write(atob(this.getAttribute('data-html')));this.contentDocument.close();" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>




```python

```
