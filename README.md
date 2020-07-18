# Transition-of-World-population

## 1. Project Overview 

### 1.1 Motivation
While I was reading Yuval Noah Harar's book called 'Homo sapiens', I was curious about how amount of people existed on the planet Earth and wanted to visualize the world's annual population change on the map. As a designer who believes that collaboration with computers will enable optimzed  design through large amounts of data, this project will be the beginning of such work.


### 1.2 Feature

You can see the results with GIF below 

- Heatmap (Pydeck) : Intensity of heatmap changes depending on population by timeline

![heatmap](https://user-images.githubusercontent.com/64841056/85198195-a3b40c80-b321-11ea-9ee6-dd67a64e4ae8.gif)

- Colormap (Pydeck) : Color of polygon in each country changes according to the number of people by timeline. 

(GIF is now preparing)

- Colormap (Kepler) : Users can easily customize layer types, colors, and so on. 
![colormap](https://user-images.githubusercontent.com/64841056/85198227-e0800380-b321-11ea-90af-6e2e69ddc379.gif)




## 2. Usage 

This usage is for heatmap layer with pydeck


- **0. Set Mapbox API** 

You need to set MAPBOX API token in order to see the map. 
Make an account and log-in to Mapbox homepage and get API access token.
Add to environment variable like :

```
 export MAPBOX_API_KEY="Your MapboxAPI token"
```


- **1.Executing Program**

```

```



- **2.Option description**
```

```



- **3. Usable Format **

CSV files are needed 

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
