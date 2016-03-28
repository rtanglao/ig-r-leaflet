# ig-r-leaflet
instagram maps using R and leaflet.js

## March 27, 2016

make a "simple map" using leaflet and
~rtanglao/Dropbox/GIT/rtgram/13March2016-abbreviated-instagram-vancouver-top-colour-lat-long-date-2015.csv

1. install leaflet and required packages
 
 ```R
 install.packages("leaflet")
 library(leaflet)
 install.packages("magrittr")
 library(magrittr)
 install.packages("webshot")
 library(webshot)
 library(htmlwidgets)
 ```
 
1. load data

 ```R
 f="~rtanglao/Dropbox/GIT/rtgram/13March2016-instagram-vancouver-top-colour-lat-long-date-2015.csv"
 data6 = read.csv(file=f,stringsAsFactors=F)
```

1. make the map

 ```R
 m <- leaflet(data6, width = 1920, height = 1080,) %>%  
 addProviderTiles("CartoDB.DarkMatterNoLabels") %>%
 setView(lng = -123.1188747,
         lat = 49.2780045,
         zoom = 14) %>%
 addCircleMarkers(
    lng = ~long, lat = ~lat,
    radius = 1,
    color = I(data6$color),
    stroke = FALSE, fillOpacity = 0.5
  )
 ```
 
 2. save to PNG

  ```R
  saveWidget(m, 'temp.html', selfcontained = FALSE)
  webshot('temp.html', file='28march2016-ig-van-cartodbdarkmatternolables-topcolour.png',
  cliprect = 'viewport')
  ```