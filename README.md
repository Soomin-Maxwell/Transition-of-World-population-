# Transition-of-World-population

## 1. Project Overview 

### 1.1 Motivation
While I was reading Yuval Noah Harar's book called 'Homo sapiens', I was curious about how amount of people existed on the planet Earth and wanted to visualize the world's annual population change on the map. As a designer who believes that collaboration with computers will enable optimzed  design through large amounts of data, this project will be the beginning of such work.


### 1.2 Feature

You can see the results with GIF below 

- Heatmap (Pydeck) : Intensity of heatmap changes depending on population by timeline

![heatmap](https://user-images.githubusercontent.com/64841056/85198195-a3b40c80-b321-11ea-9ee6-dd67a64e4ae8.gif)

- Colormap (Pydeck) : Color of polygon in each country changes according to the number of people by timeline. 

- Colormap (Kepler) : Users can easily customize layer types, colors, and so on. 




## 2. Usage 

This usage is for heatmap layer with pydeck

- **0. Executing Program** :

```

```



- **1. Import library** :

```
import csv
import pandas as pd
import geopandas as gpd
import pydeck as pdk
```   
    
- **2. Add data** :

```
# Upload data of each countries' population.
df1 = pd.read_csv("projected-population-by-country.csv")
df1.head(10)

# Upload data of each countries' latitude and longtitude. 
df2 = "countries.csv"
df2 = pd.read_csv(df2)
df2.head(10)
```  
    
- **3. Data Preprocessing** :


```
# Merge two datas.
merged = df2.merge(df1, left_on = 'name', right_on = 'Entity', how = 'left')
    
# Get data before 2021
merged = merged.loc[merged["Year"] < '2021', :] 
    
# change object -> value 
merged['Year'] = merged['Year'].astype(int)
merged['Population'] = merged['Population'].astype(int)

# NAN -> string
merged.fillna('No data', inplace = True)

# Nomalize population
merged['normal'] = merged['Population'] / merged['Population'].max()
	
# Delete column "country, entity, code"
merged.drop(["country", 'Entity', 'Code'], axis='columns', inplace=True)
```   
   

- **4. Render** :

``` 
initial_data = merged[merged['Year'] == 1800].to_dict(orient= 'records')

# Set layers 
layer = pdk.Layer(
    	"HeatmapLayer",
    	initial_data,
    	opacity=0.8,
    	get_position=["longitude", "latitude"],
    	aggregation="ADD",
    	get_weight="normal",
    	auto_highlight=True,
    	pickable=True,
    	get_radius=200)

center = [1.6015540000000001, 42.546245] 
view_state = pdk.ViewState( longitude=center[0], latitude=center[1], zoom=1) # Render 
r = pdk.Deck(
	 layers=[layer], 
	 initial_view_state = view_state ,
	 views=[pdk.View(type='MapView', controller=None)],
 	 tooltip={
 	    'html': '<b>Nation:</b> {name}',
 	    'style': {
  	  'color': 'white'
  	      }
  	  }
	)
``` 


- **5. Add slider** :

``` 
# Make widgets 
import ipywidgets as widgets
from IPython.display import display
slider = widgets.IntSlider(1800, min=1800, max=2020, step=2)

# Define functions for slider 
def on_change(v):
  results = merged[merged['Year'] == slider.value].to_dict(orient='records')
  layer.data = results
 	r.update()
    
# Connect deck with slider 
display(slider)
slider.observe(on_change)
``` 
	



## 3. Dependency 
- macOS : Catalina 10.15.5
- python : ver. 3.6.9
- pydeck : ver. 0.3.1
- pandas : 1.0.1
- geopandas : 0.7.0
- kepler.gl : 0.2.0


## 4. Reference 

[Data from "Our world in data"](https://ourworldindata.org/)  
[Pydeck github](https://github.com/visgl/deck.gl/tree/master/bindings/pydeck])  
[Kepler.gl website](https://kepler.gl/)


## 5. Version 
Current up-to-date version : v1.0.0
