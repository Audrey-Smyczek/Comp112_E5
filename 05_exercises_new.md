---
title: 'Weekly Exercises #5'
author: "Audrey Smyczek"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
## ✓ tibble  3.1.6     ✓ dplyr   1.0.7
## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
## ✓ readr   2.1.1     ✓ forcats 0.5.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(openintro)     # for the abbr2state() function
```

```
## Loading required package: airports
```

```
## Loading required package: cherryblossom
```

```
## Loading required package: usdata
```

```r
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
```

```
## 
## Attaching package: 'maps'
```

```
## The following object is masked from 'package:purrr':
## 
##     map
```

```r
library(ggmap)         # for mapping points on maps
```

```
## Google's Terms of Service: https://cloud.google.com/maps-platform/terms/.
```

```
## Please cite ggmap if you use it! See citation("ggmap") for details.
```

```r
library(gplots)        # for col2hex() function
```

```
## 
## Attaching package: 'gplots'
```

```
## The following object is masked from 'package:stats':
## 
##     lowess
```

```r
library(RColorBrewer)  # for color palettes
library(viridis)
```

```
## Loading required package: viridisLite
```

```
## 
## Attaching package: 'viridis'
```

```
## The following object is masked from 'package:maps':
## 
##     unemp
```

```r
library(sf)            # for working with spatial data
```

```
## Linking to GEOS 3.9.1, GDAL 3.2.3, PROJ 7.2.1; sf_use_s2() is TRUE
```

```r
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggmap':
## 
##     wind
```

```
## The following object is masked from 'package:ggplot2':
## 
##     last_plot
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```
## The following object is masked from 'package:graphics':
## 
##     layout
```

```r
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
```

```
## 
## Attaching package: 'transformr'
```

```
## The following object is masked from 'package:sf':
## 
##     st_normalize
```

```r
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
theme_set(theme_minimal())
```


```r
# DC Train Data
data_site <- 
  "https://www.macalester.edu/~dshuman1/data/112/2014-Q4-Trips-History-Data.rds" 
Trips <- readRDS(gzcon(url(data_site)))
Stations<-read_csv("http://www.macalester.edu/~dshuman1/data/112/DC-Stations.csv")
```

```
## Rows: 347 Columns: 5
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (1): name
## dbl (4): lat, long, nbBikes, nbEmptyDocks
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 
```

```
## Rows: 32772 Columns: 13
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (4): service, departure_station, arrival_station, delay_cause
## dbl (9): year, month, journey_time_avg, total_num_trips, avg_delay_all_depar...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)
```

```
## Rows: 3210 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl  (8): lon, lat, ele, extensions, ele.num, time_hr, dist_km, speed
## dttm (2): time, hrminsec
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")
```

```
## Rows: 36 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): event
## dbl  (3): lon, lat, extensions
## lgl  (1): ele
## dttm (2): time, hrminsec
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")
```

```
## Rows: 7924 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): event
## dbl  (4): lon, lat, ele, extensions
## dttm (2): time, hrminsec
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")
```

```
## Rows: 1111 Columns: 8
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): event
## dbl  (4): lon, lat, ele, extensions
## dttm (2): time, hrminsec
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

```
## Rows: 41894 Columns: 5
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (2): state, fips
## dbl  (2): cases, deaths
## date (1): date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


## Instructions

* **For ALL graphs, you should include appropriate labels and alt text.** 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  

```r
lettuce_harvest <- garden_harvest %>% 
  filter(vegetable == "lettuce") %>% 
  group_by(variety) %>% 
  ggplot()+
    geom_bar(aes(y = variety), 
             fill = "darkgreen")+
  labs(title = "Number of Harvests per Lettuce Variety",
       x = "Number of Harvests",
       y = "")

ggplotly(lettuce_harvest)
```

```{=html}
<div id="htmlwidget-107bba10c7788871bb1e" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-107bba10c7788871bb1e">{"x":{"data":[{"orientation":"v","width":[27,29,1,3,9],"base":[0.55,1.55,2.55,3.55,4.55],"x":[13.5,14.5,0.5,1.5,4.5],"y":[0.9,0.9,0.9,0.9,0.9],"text":["count: 27<br />variety: 0.9","count: 29<br />variety: 0.9","count:  1<br />variety: 0.9","count:  3<br />variety: 0.9","count:  9<br />variety: 0.9"],"type":"bar","textposition":"none","marker":{"autocolorscale":false,"color":"rgba(0,100,0,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":40.1826484018265,"l":133.698630136986},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Number of Harvests per Lettuce Variety","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-1.45,30.45],"tickmode":"array","ticktext":["0","10","20","30"],"tickvals":[0,10,20,30],"categoryorder":"array","categoryarray":["0","10","20","30"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"Number of Harvests","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,5.6],"tickmode":"array","ticktext":["Farmer's Market Blend","Lettuce Mixture","mustard greens","reseed","Tatsoi"],"tickvals":[1,2,3,4,5],"categoryorder":"array","categoryarray":["Farmer's Market Blend","Lettuce Mixture","mustard greens","reseed","Tatsoi"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"32cbde3d470":{"y":{},"type":"bar"}},"cur_data":"32cbde3d470","visdat":{"32cbde3d470":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```


```r
Small_Trips <- Trips %>% 
  group_by(`sstation`) %>% 
  summarise(num_departures = n()) %>% 
  ungroup()

small_trips_graph <- Small_Trips %>% 
  left_join(Stations,
            by = c("sstation"="name")) %>% 
  select(`sstation`, `lat`, `long`, `num_departures`) %>% 
  ggplot()+
  geom_point(mapping = aes(x = `lat`, 
                           y = `long`,
                           color = `num_departures`))+
    labs(title = "Map of Stations based on Longitude and Latitude Positioning",
       x = "Longitude",
       y = "Latitude")

ggplotly(small_trips_graph)
```

```{=html}
<div id="htmlwidget-f218bd8ea8dd438b940e" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-f218bd8ea8dd438b940e">{"x":{"data":[{"x":[38.895914,38.920387,38.932514,38.9172,38.893028,38.897857,38.899983,38.90268,38.929464,38.905607,38.8629,38.928644,38.903819,38.933668,38.916787,38.894832,38.9003,38.987,38.900283,38.921074,38.894514,38.884,38.898069,38.9268,38.912682,38.9086,38.942016,38.9176,38.956432,38.899632,38.9375,38.947774,38.86017,38.889908,38.92333,38.897195,38.902,38.90381,38.89054,38.90985,38.88732,38.926088,38.9121,38.89841,38.90276,38.902061,38.906602,38.908142,38.85725,38.904742,38.912648,38.89968,38.927095,38.918809,38.8952,38.8896,38.902204,38.903407,38.8923,38.9003,38.900358,38.87861,38.9057,38.8743,38.915417,38.928743,38.8561,38.8564,38.8963,38.903584,38.908905,38.9154,38.894722,38.9008,38.90534,38.892459,38.901539,38.898984,null,38.90088,38.8533,null,38.9066,38.903827,38.850688,38.848441,38.846222,38.930282,38.837666,38.903582,38.884085,38.916442,38.922581,38.90774,38.922649,38.943837,38.8851,38.917622,38.881185,38.900412,38.899408,38.87501,38.887378,38.982456,38.895344,38.88412,38.889955,38.8767,38.919077,38.897222,38.90304,38.956595,38.90093,38.899972,38.864702,38.87675,38.894573,38.897324,38.912719,38.9155,38.894851,38.889988,38.8792,38.897274,null,38.8997,38.9418,38.922925,38.843222,null,38.865784,38.862669,38.873755,38.889365,38.869442,38.857866,38.802677,38.881044,38.884961,38.992375,38.894,38.889935,38.981103,38.984691,38.900413,38.814577,38.8692,39.102099,38.90375,38.917761,38.923203,38.923583,38.977933,38.975,38.88397,38.8881,38.893648,38.88786,38.863833,38.856319,38.867262,38.862478,38.920669,38.928156,38.89696,38.805648,38.844711,38.955016,38.934267,38.941154,38.892275,38.90572,38.98954,null,39.107709,39.120045,38.8573,38.894758,38.908473,38.804378,39.084125,38.990249,38.886952,38.884,38.910972,38.801111,38.884616,38.885801,38.86559,39.096312,39.099376,null,38.989724,null,38.954812,39.076331,38.9126,38.952369,39.094772,38.96115,38.961763,38.90509,39.000578,38.87887,38.9022212,38.936043,38.949662,38.999388,38.9249,38.883921,38.8601,38.866611,38.867373,38.878433,38.927497,38.927872,38.811456,38.934751,38.887312,38.88992,38.888553,38.879819,38.9346,38.895184,38.896015,39.110314,39.114688,38.805317,38.805767,38.886266,38.9319,38.894941,38.897612,38.888251,null,38.86646,38.897315,38.905707,38.8763,38.905126,38.983627,38.804718,38.887299,38.9101,38.96497,39.103091,38.898364,38.897063,38.898404,38.820932,39.083705,38.983525,null,39.095661,38.82595,38.820064,38.833077,38.89593,38.895929,38.880705,38.876393,38.880151,38.882629,38.892164,38.896923,38.893241,38.901385,38.898536,38.903732,39.123513,38.901755,38.91554,38.90706,38.912659,38.8991,38.990639,38.988562,38.897446,38.899703,38.977093,38.88412,38.999634,38.9308,38.873057,38.862303,38.871822,38.98128,39.102212,38.863897,38.8803,38.844015,38.876737,38.82175,38.803124,38.878,38.918155,38.920682,38.992679,38.964992,39.085394,39.084379,38.866471,38.8946,38.835213,38.84232,38.8444,38.854691,38.852248,38.8426,38.859254,38.8637,38.848454,38.860789,38.834108,38.847977,38.810743,39.097636,39.119765,38.839912,38.99521,38.888767,38.997653,39.094103,38.975219,38.947607,38.9059,38.869418,39.093783,38.908008,38.894919,38.887237,null,38.944551,null,38.882788,38.857803,38.938736,38.88731,38.986743,38.884734,38.880834,null,38.8904,38.889,38.8815,38.891696,38.90849],"y":[-77.026064,-77.025672,-76.992889,-77.0259,-77.026013,-77.026975,-76.991383,-77.02674,-77.027822,-77.027137,-77.0528,-76.990955,-77.0284,-76.991016,-77.028139,-76.987633,-76.9882,-77.029417,-77.029822,-77.031887,-77.031617,-76.9861,-77.031823,-77.0322,-77.031681,-77.0323,-77.032652,-77.0321,-77.032947,-77.031686,-77.0328,-77.032818,-77.049593,-76.983326,-77.0352,-76.983575,-77.03353,-77.034931,-77.08095,-77.034438,-76.983569,-77.036536,-77.0387,-77.039624,-77.03863,-77.038322,-77.038785,-77.038359,-77.05332,-77.041606,-77.041834,-77.041539,-76.978924,-77.041571,-77.0436,-76.9769,-77.04337,-77.043648,-77.0436,-77.0429,-77.012108,-77.006004,-77.0056,-77.0057,-77.012289,-77.012457,-77.0512,-77.0492,-77.045,-77.044789,-77.04478,-77.0446,-77.045128,-77.047,-77.046774,-77.046567,-77.046564,-77.078317,null,-77.048911,-77.0498,null,-77.05152,-77.053485,-77.05152,-77.051516,-77.069275,-77.055599,-77.09482,-77.067786,-76.957461,-77.0682,-77.070334,-77.071652,-77.077271,-77.077078,-77.0023,-77.01597,-77.001828,-77.001949,-77.015289,-77.0024,-77.001955,-77.091991,-77.016106,-77.017445,-77.000349,-77.0178,-77.000648,-77.019347,-77.019027,-77.019815,-77.018677,-76.998347,-77.048672,-77.02127,-77.01994,-77.022322,-77.022155,-77.0222,-77.02324,-76.995193,-76.9953,-76.994749,null,-77.023086,-77.0251,-77.042581,-76.999388,null,-76.9784,-76.994637,-77.089233,-77.077294,-77.104503,-77.05949,-77.063562,-77.111768,-77.08777,-77.100104,-76.947974,-76.93723,-77.097426,-77.094537,-76.982872,-77.052808,-76.9599,-77.200322,-77.06269,-77.04062,-77.047637,-77.050046,-77.006472,-77.01121,-77.10783,-77.09308,-77.076701,-77.094875,-77.080319,-77.11153,-77.072315,-77.086599,-77.04368,-77.02344,-77.00493,-77.05293,-76.987823,-77.069956,-77.057979,-77.062036,-77.013917,-77.022264,-77.098029,null,-77.152072,-77.156985,-77.0511,-76.997114,-76.933099,-77.060866,-77.151291,-77.02935,-76.996806,-76.995397,-77.00495,-77.068952,-77.10108,-77.097745,-76.952103,-77.192672,-77.188014,null,-77.023854,null,-77.082426,-77.141378,-77.0135,-77.002721,-77.145213,-77.088659,-77.085998,-76.9941,-77.00149,-77.1207,-77.059219,-77.024649,-77.027333,-77.031555,-77.0222,-77.116817,-76.9672,-76.985238,-76.988039,-77.03023,-76.997194,-77.043358,-77.050276,-77.074647,-77.025762,-77.071301,-77.032429,-77.037413,-76.9955,-77.054845,-77.078107,-77.182669,-77.171487,-77.049883,-77.06072,-77.022241,-77.0388,-77.09169,-77.080851,-77.049426,null,-77.04826,-77.070993,-77.003041,-77.0037,-77.056887,-77.006311,-77.043363,-77.018939,-77.0444,-77.075946,-77.196442,-77.027869,-76.947446,-77.024281,-77.053096,-77.149443,-77.095367,null,-77.159048,-77.058541,-77.057619,-77.059821,-77.089006,-77.105246,-77.08596,-77.107735,-77.107673,-77.109366,-77.079375,-77.086502,-77.086045,-76.941877,-76.931862,-76.987211,-77.15741,-77.051084,-77.03818,-77.015231,-77.017669,-77.0337,-77.100239,-77.096539,-77.009888,-77.008911,-77.094589,-77.04657,-77.109647,-77.0315,-76.971015,-77.059936,-77.107906,-77.011336,-77.177091,-76.990037,-76.9862,-77.050537,-76.994468,-77.047494,-77.040363,-76.9607,-77.004746,-76.995876,-77.029457,-77.103381,-77.145803,-77.146866,-77.076131,-77.072305,-77.094295,-77.089555,-77.085931,-77.100555,-77.105022,-77.0502,-77.063275,-77.0633,-77.084918,-77.09586,-77.087323,-77.075104,-77.044664,-77.196636,-77.166093,-77.087083,-77.02918,-77.02858,-77.034499,-77.132954,-77.016855,-77.079382,-77.0325,-77.095596,-77.202501,-76.996985,-77.046587,-77.028226,null,-77.063896,null,-77.103148,-77.086733,-77.087171,-77.01397,-77.000035,-77.093485,-77.091129,null,-77.0889,-77.0925,-77.10396,-77.0846,-77.063586],"text":["lat: 38.89591<br />long: -77.02606<br />num_departures:  2701","lat: 38.92039<br />long: -77.02567<br />num_departures:  1556","lat: 38.93251<br />long: -76.99289<br />num_departures:   726","lat: 38.91720<br />long: -77.02590<br />num_departures:  3315","lat: 38.89303<br />long: -77.02601<br />num_departures:  3182","lat: 38.89786<br />long: -77.02697<br />num_departures:  3071","lat: 38.89998<br />long: -76.99138<br />num_departures:  2362","lat: 38.90268<br />long: -77.02674<br />num_departures:  3958","lat: 38.92946<br />long: -77.02782<br />num_departures:  4602","lat: 38.90561<br />long: -77.02714<br />num_departures:  5654","lat: 38.86290<br />long: -77.05280<br />num_departures:   656","lat: 38.92864<br />long: -76.99095<br />num_departures:   394","lat: 38.90382<br />long: -77.02840<br />num_departures:  3693","lat: 38.93367<br />long: -76.99102<br />num_departures:   336","lat: 38.91679<br />long: -77.02814<br />num_departures:  4968","lat: 38.89483<br />long: -76.98763<br />num_departures:  3330","lat: 38.90030<br />long: -76.98820<br />num_departures:  3295","lat: 38.98700<br />long: -77.02942<br />num_departures:    81","lat: 38.90028<br />long: -77.02982<br />num_departures:  3288","lat: 38.92107<br />long: -77.03189<br />num_departures:  4597","lat: 38.89451<br />long: -77.03162<br />num_departures:  4035","lat: 38.88400<br />long: -76.98610<br />num_departures:  2221","lat: 38.89807<br />long: -77.03182<br />num_departures:  3655","lat: 38.92680<br />long: -77.03220<br />num_departures:  5324","lat: 38.91268<br />long: -77.03168<br />num_departures:  5928","lat: 38.90860<br />long: -77.03230<br />num_departures:  5646","lat: 38.94202<br />long: -77.03265<br />num_departures:  1114","lat: 38.91760<br />long: -77.03210<br />num_departures:  8445","lat: 38.95643<br />long: -77.03295<br />num_departures:   806","lat: 38.89963<br />long: -77.03169<br />num_departures:  2836","lat: 38.93750<br />long: -77.03280<br />num_departures:  2368","lat: 38.94777<br />long: -77.03282<br />num_departures:   572","lat: 38.86017<br />long: -77.04959<br />num_departures:   679","lat: 38.88991<br />long: -76.98333<br />num_departures:  1861","lat: 38.92333<br />long: -77.03520<br />num_departures:  3769","lat: 38.89720<br />long: -76.98358<br />num_departures:  1574","lat: 38.90200<br />long: -77.03353<br />num_departures:  3121","lat: 38.90381<br />long: -77.03493<br />num_departures:  2884","lat: 38.89054<br />long: -77.08095<br />num_departures:   666","lat: 38.90985<br />long: -77.03444<br />num_departures:  9123","lat: 38.88732<br />long: -76.98357<br />num_departures:  2173","lat: 38.92609<br />long: -77.03654<br />num_departures:  5468","lat: 38.91210<br />long: -77.03870<br />num_departures:  7918","lat: 38.89841<br />long: -77.03962<br />num_departures:  3588","lat: 38.90276<br />long: -77.03863<br />num_departures:  5196","lat: 38.90206<br />long: -77.03832<br />num_departures:  3891","lat: 38.90660<br />long: -77.03879<br />num_departures:  4849","lat: 38.90814<br />long: -77.03836<br />num_departures:  5822","lat: 38.85725<br />long: -77.05332<br />num_departures:   403","lat: 38.90474<br />long: -77.04161<br />num_departures:  3622","lat: 38.91265<br />long: -77.04183<br />num_departures:  1543","lat: 38.89968<br />long: -77.04154<br />num_departures:  3722","lat: 38.92710<br />long: -76.97892<br />num_departures:   194","lat: 38.91881<br />long: -77.04157<br />num_departures:  4390","lat: 38.89520<br />long: -77.04360<br />num_departures:  1180","lat: 38.88960<br />long: -76.97690<br />num_departures:  1504","lat: 38.90220<br />long: -77.04337<br />num_departures:  2265","lat: 38.90341<br />long: -77.04365<br />num_departures:  2805","lat: 38.89230<br />long: -77.04360<br />num_departures:  3056","lat: 38.90030<br />long: -77.04290<br />num_departures:  2530","lat: 38.90036<br />long: -77.01211<br />num_departures:  2034","lat: 38.87861<br />long: -77.00600<br />num_departures:  3100","lat: 38.90570<br />long: -77.00560<br />num_departures:  5760","lat: 38.87430<br />long: -77.00570<br />num_departures:   580","lat: 38.91542<br />long: -77.01229<br />num_departures:  3547","lat: 38.92874<br />long: -77.01246<br />num_departures:   760","lat: 38.85610<br />long: -77.05120<br />num_departures:   332","lat: 38.85640<br />long: -77.04920<br />num_departures:   756","lat: 38.89630<br />long: -77.04500<br />num_departures:  2868","lat: 38.90358<br />long: -77.04479<br />num_departures:  2197","lat: 38.90890<br />long: -77.04478<br />num_departures:  4725","lat: 38.91540<br />long: -77.04460<br />num_departures:  6076","lat: 38.89472<br />long: -77.04513<br />num_departures:  1106","lat: 38.90080<br />long: -77.04700<br />num_departures:  3537","lat: 38.90534<br />long: -77.04677<br />num_departures:  5314","lat: 38.89246<br />long: -77.04657<br />num_departures:  2335","lat: 38.90154<br />long: -77.04656<br />num_departures:  2332","lat: 38.89898<br />long: -77.07832<br />num_departures:    94","lat:       NA<br />long:        NA<br />num_departures:   505","lat: 38.90088<br />long: -77.04891<br />num_departures:  4855","lat: 38.85330<br />long: -77.04980<br />num_departures:   971","lat:       NA<br />long:        NA<br />num_departures:  2163","lat: 38.90660<br />long: -77.05152<br />num_departures:  3028","lat: 38.90383<br />long: -77.05348<br />num_departures:  4738","lat: 38.85069<br />long: -77.05152<br />num_departures:   324","lat: 38.84844<br />long: -77.05152<br />num_departures:  1227","lat: 38.84622<br />long: -77.06928<br />num_departures:   143","lat: 38.93028<br />long: -77.05560<br />num_departures:  1849","lat: 38.83767<br />long: -77.09482<br />num_departures:    64","lat: 38.90358<br />long: -77.06779<br />num_departures:  1416","lat: 38.88408<br />long: -76.95746<br />num_departures:    13","lat: 38.91644<br />long: -77.06820<br />num_departures:  1657","lat: 38.92258<br />long: -77.07033<br />num_departures:  1338","lat: 38.90774<br />long: -77.07165<br />num_departures:  3681","lat: 38.92265<br />long: -77.07727<br />num_departures:  2145","lat: 38.94384<br />long: -77.07708<br />num_departures:  1220","lat: 38.88510<br />long: -77.00230<br />num_departures:  3290","lat: 38.91762<br />long: -77.01597<br />num_departures:  2405","lat: 38.88119<br />long: -77.00183<br />num_departures:  2249","lat: 38.90041<br />long: -77.00195<br />num_departures:  4983","lat: 38.89941<br />long: -77.01529<br />num_departures:  2431","lat: 38.87501<br />long: -77.00240<br />num_departures:  1520","lat: 38.88738<br />long: -77.00195<br />num_departures:  3492","lat: 38.98246<br />long: -77.09199<br />num_departures:   211","lat: 38.89534<br />long: -77.01611<br />num_departures:  2094","lat: 38.88412<br />long: -77.01744<br />num_departures:  3184","lat: 38.88996<br />long: -77.00035<br />num_departures:  3553","lat: 38.87670<br />long: -77.01780<br />num_departures:  4023","lat: 38.91908<br />long: -77.00065<br />num_departures:  1069","lat: 38.89722<br />long: -77.01935<br />num_departures:  3357","lat: 38.90304<br />long: -77.01903<br />num_departures:  5743","lat: 38.95660<br />long: -77.01981<br />num_departures:   320","lat: 38.90093<br />long: -77.01868<br />num_departures:  5680","lat: 38.89997<br />long: -76.99835<br />num_departures:  2738","lat: 38.86470<br />long: -77.04867<br />num_departures:   186","lat: 38.87675<br />long: -77.02127<br />num_departures:   944","lat: 38.89457<br />long: -77.01994<br />num_departures:  3176","lat: 38.89732<br />long: -77.02232<br />num_departures:  2850","lat: 38.91272<br />long: -77.02215<br />num_departures:  5009","lat: 38.91550<br />long: -77.02220<br />num_departures:  4889","lat: 38.89485<br />long: -77.02324<br />num_departures:  3191","lat: 38.88999<br />long: -76.99519<br />num_departures:  2474","lat: 38.87920<br />long: -76.99530<br />num_departures:  1285","lat: 38.89727<br />long: -76.99475<br />num_departures:  2921","lat:       NA<br />long:        NA<br />num_departures:  1317","lat: 38.89970<br />long: -77.02309<br />num_departures:  5748","lat: 38.94180<br />long: -77.02510<br />num_departures:  1360","lat: 38.92292<br />long: -77.04258<br />num_departures:  6373","lat: 38.84322<br />long: -76.99939<br />num_departures:    52","lat:       NA<br />long:        NA<br />num_departures:   214","lat: 38.86578<br />long: -76.97840<br />num_departures:   104","lat: 38.86267<br />long: -76.99464<br />num_departures:   412","lat: 38.87376<br />long: -77.08923<br />num_departures:   161","lat: 38.88936<br />long: -77.07729<br />num_departures:   496","lat: 38.86944<br />long: -77.10450<br />num_departures:   457","lat: 38.85787<br />long: -77.05949<br />num_departures:   579","lat: 38.80268<br />long: -77.06356<br />num_departures:   673","lat: 38.88104<br />long: -77.11177<br />num_departures:  1558","lat: 38.88496<br />long: -77.08777<br />num_departures:   416","lat: 38.99238<br />long: -77.10010<br />num_departures:   261","lat: 38.89400<br />long: -76.94797<br />num_departures:    89","lat: 38.88994<br />long: -76.93723<br />num_departures:   121","lat: 38.98110<br />long: -77.09743<br />num_departures:   397","lat: 38.98469<br />long: -77.09454<br />num_departures:   896","lat: 38.90041<br />long: -76.98287<br />num_departures:  1375","lat: 38.81458<br />long: -77.05281<br />num_departures:  1629","lat: 38.86920<br />long: -76.95990<br />num_departures:    38","lat: 39.10210<br />long: -77.20032<br />num_departures:     8","lat: 38.90375<br />long: -77.06269<br />num_departures:  3324","lat: 38.91776<br />long: -77.04062<br />num_departures:  4031","lat: 38.92320<br />long: -77.04764<br />num_departures:  1553","lat: 38.92358<br />long: -77.05005<br />num_departures:  5381","lat: 38.97793<br />long: -77.00647<br />num_departures:   555","lat: 38.97500<br />long: -77.01121<br />num_departures:   374","lat: 38.88397<br />long: -77.10783<br />num_departures:   576","lat: 38.88810<br />long: -77.09308<br />num_departures:   602","lat: 38.89365<br />long: -77.07670<br />num_departures:   822","lat: 38.88786<br />long: -77.09488<br />num_departures:  1277","lat: 38.86383<br />long: -77.08032<br />num_departures:   496","lat: 38.85632<br />long: -77.11153<br />num_departures:   123","lat: 38.86726<br />long: -77.07232<br />num_departures:   246","lat: 38.86248<br />long: -77.08660<br />num_departures:   369","lat: 38.92067<br />long: -77.04368<br />num_departures:  3657","lat: 38.92816<br />long: -77.02344<br />num_departures:  2578","lat: 38.89696<br />long: -77.00493<br />num_departures: 15876","lat: 38.80565<br />long: -77.05293<br />num_departures:   363","lat: 38.84471<br />long: -76.98782<br />num_departures:    85","lat: 38.95502<br />long: -77.06996<br />num_departures:  1079","lat: 38.93427<br />long: -77.05798<br />num_departures:  1783","lat: 38.94115<br />long: -77.06204<br />num_departures:   983","lat: 38.89227<br />long: -77.01392<br />num_departures:  3022","lat: 38.90572<br />long: -77.02226<br />num_departures:  5181","lat: 38.98954<br />long: -77.09803<br />num_departures:   345","lat:       NA<br />long:        NA<br />num_departures:  1652","lat: 39.10771<br />long: -77.15207<br />num_departures:    96","lat: 39.12004<br />long: -77.15699<br />num_departures:     4","lat: 38.85730<br />long: -77.05110<br />num_departures:  2468","lat: 38.89476<br />long: -76.99711<br />num_departures:  3807","lat: 38.90847<br />long: -76.93310<br />num_departures:    29","lat: 38.80438<br />long: -77.06087<br />num_departures:   192","lat: 39.08413<br />long: -77.15129<br />num_departures:    56","lat: 38.99025<br />long: -77.02935<br />num_departures:   240","lat: 38.88695<br />long: -76.99681<br />num_departures:  3583","lat: 38.88400<br />long: -76.99540<br />num_departures:  6982","lat: 38.91097<br />long: -77.00495<br />num_departures:  1994","lat: 38.80111<br />long: -77.06895<br />num_departures:   186","lat: 38.88462<br />long: -77.10108<br />num_departures:   619","lat: 38.88580<br />long: -77.09775<br />num_departures:   761","lat: 38.86559<br />long: -76.95210<br />num_departures:    11","lat: 39.09631<br />long: -77.19267<br />num_departures:    46","lat: 39.09938<br />long: -77.18801<br />num_departures:    11","lat:       NA<br />long:        NA<br />num_departures:   188","lat: 38.98972<br />long: -77.02385<br />num_departures:   252","lat:       NA<br />long:        NA<br />num_departures:   397","lat: 38.95481<br />long: -77.08243<br />num_departures:   225","lat: 39.07633<br />long: -77.14138<br />num_departures:    46","lat: 38.91260<br />long: -77.01350<br />num_departures:  3658","lat: 38.95237<br />long: -77.00272<br />num_departures:   175","lat: 39.09477<br />long: -77.14521<br />num_departures:    61","lat: 38.96115<br />long: -77.08866<br />num_departures:   214","lat: 38.96176<br />long: -77.08600<br />num_departures:   584","lat: 38.90509<br />long: -76.99410<br />num_departures:  1607","lat: 39.00058<br />long: -77.00149<br />num_departures:    34","lat: 38.87887<br />long: -77.12070<br />num_departures:   503","lat: 38.90222<br />long: -77.05922<br />num_departures:  2728","lat: 38.93604<br />long: -77.02465<br />num_departures:  3353","lat: 38.94966<br />long: -77.02733<br />num_departures:   562","lat: 38.99939<br />long: -77.03155<br />num_departures:   103","lat: 38.92490<br />long: -77.02220<br />num_departures:  1322","lat: 38.88392<br />long: -77.11682<br />num_departures:   434","lat: 38.86010<br />long: -76.96720<br />num_departures:    77","lat: 38.86661<br />long: -76.98524<br />num_departures:   180","lat: 38.86737<br />long: -76.98804<br />num_departures:   252","lat: 38.87843<br />long: -77.03023<br />num_departures:   746","lat: 38.92750<br />long: -76.99719<br />num_departures:   495","lat: 38.92787<br />long: -77.04336<br />num_departures:   798","lat: 38.81146<br />long: -77.05028<br />num_departures:   236","lat: 38.93475<br />long: -77.07465<br />num_departures:  1217","lat: 38.88731<br />long: -77.02576<br />num_departures:  1499","lat: 38.88992<br />long: -77.07130<br />num_departures:  1388","lat: 38.88855<br />long: -77.03243<br />num_departures:  8207","lat: 38.87982<br />long: -77.03741<br />num_departures:  5160","lat: 38.93460<br />long: -76.99550<br />num_departures:   561","lat: 38.89518<br />long: -77.05485<br />num_departures:   853","lat: 38.89601<br />long: -77.07811<br />num_departures:   526","lat: 39.11031<br />long: -77.18267<br />num_departures:    97","lat: 39.11469<br />long: -77.17149<br />num_departures:   155","lat: 38.80532<br />long: -77.04988<br />num_departures:   669","lat: 38.80577<br />long: -77.06072<br />num_departures:  1423","lat: 38.88627<br />long: -77.02224<br />num_departures:  3784","lat: 38.93190<br />long: -77.03880<br />num_departures:  4496","lat: 38.89494<br />long: -77.09169<br />num_departures:   565","lat: 38.89761<br />long: -77.08085<br />num_departures:   785","lat: 38.88825<br />long: -77.04943<br />num_departures:  9984","lat:       NA<br />long:        NA<br />num_departures:  3942","lat: 38.86646<br />long: -77.04826<br />num_departures:   131","lat: 38.89731<br />long: -77.07099<br />num_departures:  2621","lat: 38.90571<br />long: -77.00304<br />num_departures:  3652","lat: 38.87630<br />long: -77.00370<br />num_departures:  1606","lat: 38.90513<br />long: -77.05689<br />num_departures:  4380","lat: 38.98363<br />long: -77.00631<br />num_departures:   130","lat: 38.80472<br />long: -77.04336<br />num_departures:   742","lat: 38.88730<br />long: -77.01894<br />num_departures:  4742","lat: 38.91010<br />long: -77.04440<br />num_departures: 13056","lat: 38.96497<br />long: -77.07595<br />num_departures:   210","lat: 39.10309<br />long: -77.19644<br />num_departures:    39","lat: 38.89836<br />long: -77.02787<br />num_departures:  4321","lat: 38.89706<br />long: -76.94745<br />num_departures:    96","lat: 38.89840<br />long: -77.02428<br />num_departures:  2239","lat: 38.82093<br />long: -77.05310<br />num_departures:   313","lat: 39.08371<br />long: -77.14944<br />num_departures:    45","lat: 38.98353<br />long: -77.09537<br />num_departures:   316","lat:       NA<br />long:        NA<br />num_departures:   158","lat: 39.09566<br />long: -77.15905<br />num_departures:    49","lat: 38.82595<br />long: -77.05854<br />num_departures:   447","lat: 38.82006<br />long: -77.05762<br />num_departures:   467","lat: 38.83308<br />long: -77.05982<br />num_departures:   277","lat: 38.89593<br />long: -77.08901<br />num_departures:  1198","lat: 38.89593<br />long: -77.10525<br />num_departures:    28","lat: 38.88070<br />long: -77.08596<br />num_departures:   479","lat: 38.87639<br />long: -77.10774<br />num_departures:   668","lat: 38.88015<br />long: -77.10767<br />num_departures:  1043","lat: 38.88263<br />long: -77.10937<br />num_departures:   732","lat: 38.89216<br />long: -77.07937<br />num_departures:   478","lat: 38.89692<br />long: -77.08650<br />num_departures:   718","lat: 38.89324<br />long: -77.08604<br />num_departures:   593","lat: 38.90138<br />long: -76.94188<br />num_departures:    35","lat: 38.89854<br />long: -76.93186<br />num_departures:    61","lat: 38.90373<br />long: -76.98721<br />num_departures:  1368","lat: 39.12351<br />long: -77.15741<br />num_departures:     4","lat: 38.90176<br />long: -77.05108<br />num_departures:  2729","lat: 38.91554<br />long: -77.03818<br />num_departures:  9077","lat: 38.90706<br />long: -77.01523<br />num_departures:  2418","lat: 38.91266<br />long: -77.01767<br />num_departures:  2403","lat: 38.89910<br />long: -77.03370<br />num_departures:  4784","lat: 38.99064<br />long: -77.10024<br />num_departures:   186","lat: 38.98856<br />long: -77.09654<br />num_departures:   272","lat: 38.89745<br />long: -77.00989<br />num_departures:  6196","lat: 38.89970<br />long: -77.00891<br />num_departures:  1902","lat: 38.97709<br />long: -77.09459<br />num_departures:   334","lat: 38.88412<br />long: -77.04657<br />num_departures:  2341","lat: 38.99963<br />long: -77.10965<br />num_departures:   204","lat: 38.93080<br />long: -77.03150<br />num_departures:  6052","lat: 38.87306<br />long: -76.97101<br />num_departures:   151","lat: 38.86230<br />long: -77.05994<br />num_departures:  1351","lat: 38.87182<br />long: -77.10791<br />num_departures:   627","lat: 38.98128<br />long: -77.01134<br />num_departures:   238","lat: 39.10221<br />long: -77.17709<br />num_departures:    22","lat: 38.86390<br />long: -76.99004<br />num_departures:   190","lat: 38.88030<br />long: -76.98620<br />num_departures:  2124","lat: 38.84401<br />long: -77.05054<br />num_departures:   380","lat: 38.87674<br />long: -76.99447<br />num_departures:   473","lat: 38.82175<br />long: -77.04749<br />num_departures:   362","lat: 38.80312<br />long: -77.04036<br />num_departures:   427","lat: 38.87800<br />long: -76.96070<br />num_departures:     9","lat: 38.91815<br />long: -77.00475<br />num_departures:  1400","lat: 38.92068<br />long: -76.99588<br />num_departures:   456","lat: 38.99268<br />long: -77.02946<br />num_departures:   140","lat: 38.96499<br />long: -77.10338<br />num_departures:   290","lat: 39.08539<br />long: -77.14580<br />num_departures:    94","lat: 39.08438<br />long: -77.14687<br />num_departures:    78","lat: 38.86647<br />long: -77.07613<br />num_departures:    99","lat: 38.89460<br />long: -77.07231<br />num_departures:  1580","lat: 38.83521<br />long: -77.09430<br />num_departures:    11","lat: 38.84232<br />long: -77.08956<br />num_departures:   359","lat: 38.84440<br />long: -77.08593<br />num_departures:    99","lat: 38.85469<br />long: -77.10055<br />num_departures:    14","lat: 38.85225<br />long: -77.10502<br />num_departures:    86","lat: 38.84260<br />long: -77.05020<br />num_departures:   667","lat: 38.85925<br />long: -77.06328<br />num_departures:   197","lat: 38.86370<br />long: -77.06330<br />num_departures:   838","lat: 38.84845<br />long: -77.08492<br />num_departures:    59","lat: 38.86079<br />long: -77.09586<br />num_departures:    23","lat: 38.83411<br />long: -77.08732<br />num_departures:   104","lat: 38.84798<br />long: -77.07510<br />num_departures:   158","lat: 38.81074<br />long: -77.04466<br />num_departures:   527","lat: 39.09764<br />long: -77.19664<br />num_departures:     2","lat: 39.11977<br />long: -77.16609<br />num_departures:   315","lat: 38.83991<br />long: -77.08708<br />num_departures:    67","lat: 38.99521<br />long: -77.02918<br />num_departures:   143","lat: 38.88877<br />long: -77.02858<br />num_departures:  5120","lat: 38.99765<br />long: -77.03450<br />num_departures:    22","lat: 39.09410<br />long: -77.13295<br />num_departures:     8","lat: 38.97522<br />long: -77.01686<br />num_departures:  1585","lat: 38.94761<br />long: -77.07938<br />num_departures:  2189","lat: 38.90590<br />long: -77.03250<br />num_departures:  9597","lat: 38.86942<br />long: -77.09560<br />num_departures:   331","lat: 39.09378<br />long: -77.20250<br />num_departures:    10","lat: 38.90801<br />long: -76.99698<br />num_departures:   284","lat: 38.89492<br />long: -77.04659<br />num_departures:  2165","lat: 38.88724<br />long: -77.02823<br />num_departures:  3150","lat:       NA<br />long:        NA<br />num_departures:   307","lat: 38.94455<br />long: -77.06390<br />num_departures:  1372","lat:       NA<br />long:        NA<br />num_departures:    85","lat: 38.88279<br />long: -77.10315<br />num_departures:  1614","lat: 38.85780<br />long: -77.08673<br />num_departures:    67","lat: 38.93874<br />long: -77.08717<br />num_departures:  1312","lat: 38.88731<br />long: -77.01397<br />num_departures:  3413","lat: 38.98674<br />long: -77.00003<br />num_departures:   206","lat: 38.88473<br />long: -77.09349<br />num_departures:   592","lat: 38.88083<br />long: -77.09113<br />num_departures:   232","lat:       NA<br />long:        NA<br />num_departures:   173","lat: 38.89040<br />long: -77.08890<br />num_departures:   887","lat: 38.88900<br />long: -77.09250<br />num_departures:   770","lat: 38.88150<br />long: -77.10396<br />num_departures:   405","lat: 38.89170<br />long: -77.08460<br />num_departures:  1589","lat: 38.90849<br />long: -77.06359<br />num_departures:  2517"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":["rgba(29,63,95,1)","rgba(25,55,83,1)","rgba(22,48,74,1)","rgba(32,68,101,1)","rgba(31,67,100,1)","rgba(31,66,98,1)","rgba(28,61,91,1)","rgba(34,73,108,1)","rgba(37,78,115,1)","rgba(41,87,126,1)","rgba(21,48,74,1)","rgba(20,46,71,1)","rgba(33,71,105,1)","rgba(20,45,70,1)","rgba(38,81,119,1)","rgba(32,68,101,1)","rgba(32,68,101,1)","rgba(19,44,68,1)","rgba(32,68,101,1)","rgba(37,78,115,1)","rgba(35,74,109,1)","rgba(27,60,90,1)","rgba(33,71,105,1)","rgba(40,84,123,1)","rgba(42,89,129,1)","rgba(41,87,126,1)","rgba(23,51,78,1)","rgba(53,110,158,1)","rgba(22,49,75,1)","rgba(30,64,96,1)","rgba(28,61,91,1)","rgba(21,47,73,1)","rgba(22,48,74,1)","rgba(26,57,86,1)","rgba(34,72,106,1)","rgba(25,55,83,1)","rgba(31,67,99,1)","rgba(30,65,96,1)","rgba(21,48,74,1)","rgba(56,116,166,1)","rgba(27,59,89,1)","rgba(40,86,124,1)","rgba(51,106,152,1)","rgba(33,70,104,1)","rgba(39,83,121,1)","rgba(34,73,107,1)","rgba(38,80,117,1)","rgba(42,88,128,1)","rgba(21,46,71,1)","rgba(33,71,104,1)","rgba(25,55,83,1)","rgba(33,71,105,1)","rgba(20,44,69,1)","rgba(36,77,112,1)","rgba(23,52,79,1)","rgba(25,54,82,1)","rgba(28,60,90,1)","rgba(30,64,96,1)","rgba(31,66,98,1)","rgba(29,62,93,1)","rgba(27,58,88,1)","rgba(31,67,99,1)","rgba(42,88,127,1)","rgba(21,47,73,1)","rgba(33,70,103,1)","rgba(22,49,75,1)","rgba(20,45,70,1)","rgba(22,49,75,1)","rgba(30,65,96,1)","rgba(27,60,89,1)","rgba(37,79,116,1)","rgba(43,91,131,1)","rgba(23,51,78,1)","rgba(33,70,103,1)","rgba(40,84,123,1)","rgba(28,61,91,1)","rgba(28,61,91,1)","rgba(19,44,68,1)","rgba(21,47,72,1)","rgba(38,81,118,1)","rgba(23,50,77,1)","rgba(27,59,89,1)","rgba(31,66,98,1)","rgba(37,80,116,1)","rgba(20,45,70,1)","rgba(24,52,79,1)","rgba(20,44,68,1)","rgba(26,57,86,1)","rgba(19,43,68,1)","rgba(24,54,81,1)","rgba(19,43,67,1)","rgba(25,55,84,1)","rgba(24,53,80,1)","rgba(33,71,105,1)","rgba(27,59,89,1)","rgba(24,52,79,1)","rgba(32,68,101,1)","rgba(28,61,91,1)","rgba(28,60,90,1)","rgba(38,82,119,1)","rgba(28,61,92,1)","rgba(25,54,82,1)","rgba(32,70,103,1)","rgba(20,45,69,1)","rgba(27,59,88,1)","rgba(31,67,100,1)","rgba(33,70,104,1)","rgba(35,74,109,1)","rgba(23,51,78,1)","rgba(32,69,101,1)","rgba(42,88,127,1)","rgba(20,45,70,1)","rgba(41,87,127,1)","rgba(30,64,95,1)","rgba(20,44,69,1)","rgba(23,50,76,1)","rgba(31,67,100,1)","rgba(30,65,96,1)","rgba(39,82,119,1)","rgba(38,81,118,1)","rgba(31,67,100,1)","rgba(28,62,92,1)","rgba(24,53,80,1)","rgba(30,65,97,1)","rgba(24,53,80,1)","rgba(42,88,127,1)","rgba(24,53,81,1)","rgba(44,93,134,1)","rgba(19,43,67,1)","rgba(20,45,69,1)","rgba(19,44,68,1)","rgba(21,46,71,1)","rgba(20,44,69,1)","rgba(21,47,72,1)","rgba(21,46,72,1)","rgba(21,47,73,1)","rgba(22,48,74,1)","rgba(25,55,83,1)","rgba(21,46,71,1)","rgba(20,45,70,1)","rgba(19,44,68,1)","rgba(19,44,68,1)","rgba(20,46,71,1)","rgba(22,50,76,1)","rgba(24,53,81,1)","rgba(25,55,83,1)","rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(32,68,101,1)","rgba(35,74,109,1)","rgba(25,55,83,1)","rgba(40,85,123,1)","rgba(21,47,73,1)","rgba(20,46,71,1)","rgba(21,47,73,1)","rgba(21,47,73,1)","rgba(22,49,75,1)","rgba(24,52,80,1)","rgba(21,47,72,1)","rgba(19,44,68,1)","rgba(20,45,69,1)","rgba(20,46,71,1)","rgba(33,71,105,1)","rgba(29,62,93,1)","rgba(86,177,247,1)","rgba(20,46,71,1)","rgba(19,44,68,1)","rgba(23,51,78,1)","rgba(26,56,85,1)","rgba(23,50,77,1)","rgba(31,66,98,1)","rgba(39,83,121,1)","rgba(20,46,70,1)","rgba(25,55,84,1)","rgba(19,44,68,1)","rgba(19,43,67,1)","rgba(28,62,92,1)","rgba(34,72,106,1)","rgba(19,43,67,1)","rgba(20,44,69,1)","rgba(19,43,68,1)","rgba(20,45,69,1)","rgba(33,70,104,1)","rgba(47,98,141,1)","rgba(27,58,87,1)","rgba(20,44,69,1)","rgba(21,48,73,1)","rgba(22,49,75,1)","rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(20,44,69,1)","rgba(20,45,69,1)","rgba(20,46,71,1)","rgba(20,45,69,1)","rgba(19,43,67,1)","rgba(33,71,105,1)","rgba(20,44,69,1)","rgba(19,43,68,1)","rgba(20,45,69,1)","rgba(21,47,73,1)","rgba(25,55,83,1)","rgba(19,43,67,1)","rgba(21,47,72,1)","rgba(29,64,95,1)","rgba(32,69,101,1)","rgba(21,47,73,1)","rgba(19,44,68,1)","rgba(24,53,80,1)","rgba(21,46,71,1)","rgba(19,44,68,1)","rgba(20,44,69,1)","rgba(20,45,69,1)","rgba(22,48,74,1)","rgba(21,47,72,1)","rgba(22,49,75,1)","rgba(20,45,69,1)","rgba(24,52,79,1)","rgba(25,54,82,1)","rgba(24,53,81,1)","rgba(52,108,155,1)","rgba(39,83,121,1)","rgba(21,47,73,1)","rgba(22,49,75,1)","rgba(21,47,72,1)","rgba(19,44,68,1)","rgba(20,44,69,1)","rgba(22,48,74,1)","rgba(24,54,81,1)","rgba(34,72,106,1)","rgba(37,78,114,1)","rgba(21,47,73,1)","rgba(22,49,75,1)","rgba(60,124,176,1)","rgba(34,73,108,1)","rgba(19,44,68,1)","rgba(29,63,94,1)","rgba(33,71,105,1)","rgba(25,55,83,1)","rgba(36,77,112,1)","rgba(19,44,68,1)","rgba(22,48,74,1)","rgba(38,80,116,1)","rgba(73,151,212,1)","rgba(20,45,69,1)","rgba(19,43,67,1)","rgba(36,76,112,1)","rgba(19,44,68,1)","rgba(28,60,90,1)","rgba(20,45,70,1)","rgba(19,43,67,1)","rgba(20,45,70,1)","rgba(20,44,69,1)","rgba(19,43,67,1)","rgba(21,46,71,1)","rgba(21,46,72,1)","rgba(20,45,70,1)","rgba(24,52,79,1)","rgba(19,43,67,1)","rgba(21,47,72,1)","rgba(22,48,74,1)","rgba(23,51,77,1)","rgba(22,48,74,1)","rgba(21,47,72,1)","rgba(22,48,74,1)","rgba(21,47,73,1)","rgba(19,43,67,1)","rgba(19,43,68,1)","rgba(24,53,81,1)","rgba(19,43,67,1)","rgba(29,64,95,1)","rgba(56,116,165,1)","rgba(28,61,92,1)","rgba(28,61,91,1)","rgba(38,80,117,1)","rgba(20,44,69,1)","rgba(20,45,70,1)","rgba(43,92,132,1)","rgba(26,57,86,1)","rgba(20,45,70,1)","rgba(28,61,91,1)","rgba(20,44,69,1)","rgba(43,90,131,1)","rgba(20,44,68,1)","rgba(24,53,81,1)","rgba(21,48,73,1)","rgba(20,45,69,1)","rgba(19,43,67,1)","rgba(20,44,69,1)","rgba(27,59,88,1)","rgba(20,46,71,1)","rgba(21,46,72,1)","rgba(20,46,71,1)","rgba(21,46,71,1)","rgba(19,43,67,1)","rgba(24,53,81,1)","rgba(21,46,72,1)","rgba(20,44,68,1)","rgba(20,45,70,1)","rgba(19,44,68,1)","rgba(19,44,68,1)","rgba(19,44,68,1)","rgba(25,55,83,1)","rgba(19,43,67,1)","rgba(20,46,71,1)","rgba(19,44,68,1)","rgba(19,43,67,1)","rgba(19,44,68,1)","rgba(22,48,74,1)","rgba(20,44,69,1)","rgba(22,49,75,1)","rgba(19,43,68,1)","rgba(19,43,67,1)","rgba(19,44,68,1)","rgba(20,44,69,1)","rgba(21,47,72,1)","rgba(19,43,67,1)","rgba(20,45,70,1)","rgba(19,43,68,1)","rgba(20,44,68,1)","rgba(39,83,120,1)","rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(25,55,83,1)","rgba(27,59,89,1)","rgba(58,120,171,1)","rgba(20,45,70,1)","rgba(19,43,67,1)","rgba(20,45,70,1)","rgba(27,59,89,1)","rgba(31,67,99,1)","rgba(20,45,70,1)","rgba(24,53,81,1)","rgba(19,44,68,1)","rgba(25,55,83,1)","rgba(19,43,68,1)","rgba(24,53,80,1)","rgba(32,69,102,1)","rgba(20,44,69,1)","rgba(21,47,73,1)","rgba(20,45,69,1)","rgba(20,44,69,1)","rgba(22,50,76,1)","rgba(22,49,75,1)","rgba(21,46,71,1)","rgba(25,55,83,1)","rgba(29,62,93,1)"],"opacity":1,"size":5.66929133858268,"symbol":"circle","line":{"width":1.88976377952756,"color":["rgba(29,63,95,1)","rgba(25,55,83,1)","rgba(22,48,74,1)","rgba(32,68,101,1)","rgba(31,67,100,1)","rgba(31,66,98,1)","rgba(28,61,91,1)","rgba(34,73,108,1)","rgba(37,78,115,1)","rgba(41,87,126,1)","rgba(21,48,74,1)","rgba(20,46,71,1)","rgba(33,71,105,1)","rgba(20,45,70,1)","rgba(38,81,119,1)","rgba(32,68,101,1)","rgba(32,68,101,1)","rgba(19,44,68,1)","rgba(32,68,101,1)","rgba(37,78,115,1)","rgba(35,74,109,1)","rgba(27,60,90,1)","rgba(33,71,105,1)","rgba(40,84,123,1)","rgba(42,89,129,1)","rgba(41,87,126,1)","rgba(23,51,78,1)","rgba(53,110,158,1)","rgba(22,49,75,1)","rgba(30,64,96,1)","rgba(28,61,91,1)","rgba(21,47,73,1)","rgba(22,48,74,1)","rgba(26,57,86,1)","rgba(34,72,106,1)","rgba(25,55,83,1)","rgba(31,67,99,1)","rgba(30,65,96,1)","rgba(21,48,74,1)","rgba(56,116,166,1)","rgba(27,59,89,1)","rgba(40,86,124,1)","rgba(51,106,152,1)","rgba(33,70,104,1)","rgba(39,83,121,1)","rgba(34,73,107,1)","rgba(38,80,117,1)","rgba(42,88,128,1)","rgba(21,46,71,1)","rgba(33,71,104,1)","rgba(25,55,83,1)","rgba(33,71,105,1)","rgba(20,44,69,1)","rgba(36,77,112,1)","rgba(23,52,79,1)","rgba(25,54,82,1)","rgba(28,60,90,1)","rgba(30,64,96,1)","rgba(31,66,98,1)","rgba(29,62,93,1)","rgba(27,58,88,1)","rgba(31,67,99,1)","rgba(42,88,127,1)","rgba(21,47,73,1)","rgba(33,70,103,1)","rgba(22,49,75,1)","rgba(20,45,70,1)","rgba(22,49,75,1)","rgba(30,65,96,1)","rgba(27,60,89,1)","rgba(37,79,116,1)","rgba(43,91,131,1)","rgba(23,51,78,1)","rgba(33,70,103,1)","rgba(40,84,123,1)","rgba(28,61,91,1)","rgba(28,61,91,1)","rgba(19,44,68,1)","rgba(21,47,72,1)","rgba(38,81,118,1)","rgba(23,50,77,1)","rgba(27,59,89,1)","rgba(31,66,98,1)","rgba(37,80,116,1)","rgba(20,45,70,1)","rgba(24,52,79,1)","rgba(20,44,68,1)","rgba(26,57,86,1)","rgba(19,43,68,1)","rgba(24,54,81,1)","rgba(19,43,67,1)","rgba(25,55,84,1)","rgba(24,53,80,1)","rgba(33,71,105,1)","rgba(27,59,89,1)","rgba(24,52,79,1)","rgba(32,68,101,1)","rgba(28,61,91,1)","rgba(28,60,90,1)","rgba(38,82,119,1)","rgba(28,61,92,1)","rgba(25,54,82,1)","rgba(32,70,103,1)","rgba(20,45,69,1)","rgba(27,59,88,1)","rgba(31,67,100,1)","rgba(33,70,104,1)","rgba(35,74,109,1)","rgba(23,51,78,1)","rgba(32,69,101,1)","rgba(42,88,127,1)","rgba(20,45,70,1)","rgba(41,87,127,1)","rgba(30,64,95,1)","rgba(20,44,69,1)","rgba(23,50,76,1)","rgba(31,67,100,1)","rgba(30,65,96,1)","rgba(39,82,119,1)","rgba(38,81,118,1)","rgba(31,67,100,1)","rgba(28,62,92,1)","rgba(24,53,80,1)","rgba(30,65,97,1)","rgba(24,53,80,1)","rgba(42,88,127,1)","rgba(24,53,81,1)","rgba(44,93,134,1)","rgba(19,43,67,1)","rgba(20,45,69,1)","rgba(19,44,68,1)","rgba(21,46,71,1)","rgba(20,44,69,1)","rgba(21,47,72,1)","rgba(21,46,72,1)","rgba(21,47,73,1)","rgba(22,48,74,1)","rgba(25,55,83,1)","rgba(21,46,71,1)","rgba(20,45,70,1)","rgba(19,44,68,1)","rgba(19,44,68,1)","rgba(20,46,71,1)","rgba(22,50,76,1)","rgba(24,53,81,1)","rgba(25,55,83,1)","rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(32,68,101,1)","rgba(35,74,109,1)","rgba(25,55,83,1)","rgba(40,85,123,1)","rgba(21,47,73,1)","rgba(20,46,71,1)","rgba(21,47,73,1)","rgba(21,47,73,1)","rgba(22,49,75,1)","rgba(24,52,80,1)","rgba(21,47,72,1)","rgba(19,44,68,1)","rgba(20,45,69,1)","rgba(20,46,71,1)","rgba(33,71,105,1)","rgba(29,62,93,1)","rgba(86,177,247,1)","rgba(20,46,71,1)","rgba(19,44,68,1)","rgba(23,51,78,1)","rgba(26,56,85,1)","rgba(23,50,77,1)","rgba(31,66,98,1)","rgba(39,83,121,1)","rgba(20,46,70,1)","rgba(25,55,84,1)","rgba(19,44,68,1)","rgba(19,43,67,1)","rgba(28,62,92,1)","rgba(34,72,106,1)","rgba(19,43,67,1)","rgba(20,44,69,1)","rgba(19,43,68,1)","rgba(20,45,69,1)","rgba(33,70,104,1)","rgba(47,98,141,1)","rgba(27,58,87,1)","rgba(20,44,69,1)","rgba(21,48,73,1)","rgba(22,49,75,1)","rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(20,44,69,1)","rgba(20,45,69,1)","rgba(20,46,71,1)","rgba(20,45,69,1)","rgba(19,43,67,1)","rgba(33,71,105,1)","rgba(20,44,69,1)","rgba(19,43,68,1)","rgba(20,45,69,1)","rgba(21,47,73,1)","rgba(25,55,83,1)","rgba(19,43,67,1)","rgba(21,47,72,1)","rgba(29,64,95,1)","rgba(32,69,101,1)","rgba(21,47,73,1)","rgba(19,44,68,1)","rgba(24,53,80,1)","rgba(21,46,71,1)","rgba(19,44,68,1)","rgba(20,44,69,1)","rgba(20,45,69,1)","rgba(22,48,74,1)","rgba(21,47,72,1)","rgba(22,49,75,1)","rgba(20,45,69,1)","rgba(24,52,79,1)","rgba(25,54,82,1)","rgba(24,53,81,1)","rgba(52,108,155,1)","rgba(39,83,121,1)","rgba(21,47,73,1)","rgba(22,49,75,1)","rgba(21,47,72,1)","rgba(19,44,68,1)","rgba(20,44,69,1)","rgba(22,48,74,1)","rgba(24,54,81,1)","rgba(34,72,106,1)","rgba(37,78,114,1)","rgba(21,47,73,1)","rgba(22,49,75,1)","rgba(60,124,176,1)","rgba(34,73,108,1)","rgba(19,44,68,1)","rgba(29,63,94,1)","rgba(33,71,105,1)","rgba(25,55,83,1)","rgba(36,77,112,1)","rgba(19,44,68,1)","rgba(22,48,74,1)","rgba(38,80,116,1)","rgba(73,151,212,1)","rgba(20,45,69,1)","rgba(19,43,67,1)","rgba(36,76,112,1)","rgba(19,44,68,1)","rgba(28,60,90,1)","rgba(20,45,70,1)","rgba(19,43,67,1)","rgba(20,45,70,1)","rgba(20,44,69,1)","rgba(19,43,67,1)","rgba(21,46,71,1)","rgba(21,46,72,1)","rgba(20,45,70,1)","rgba(24,52,79,1)","rgba(19,43,67,1)","rgba(21,47,72,1)","rgba(22,48,74,1)","rgba(23,51,77,1)","rgba(22,48,74,1)","rgba(21,47,72,1)","rgba(22,48,74,1)","rgba(21,47,73,1)","rgba(19,43,67,1)","rgba(19,43,68,1)","rgba(24,53,81,1)","rgba(19,43,67,1)","rgba(29,64,95,1)","rgba(56,116,165,1)","rgba(28,61,92,1)","rgba(28,61,91,1)","rgba(38,80,117,1)","rgba(20,44,69,1)","rgba(20,45,70,1)","rgba(43,92,132,1)","rgba(26,57,86,1)","rgba(20,45,70,1)","rgba(28,61,91,1)","rgba(20,44,69,1)","rgba(43,90,131,1)","rgba(20,44,68,1)","rgba(24,53,81,1)","rgba(21,48,73,1)","rgba(20,45,69,1)","rgba(19,43,67,1)","rgba(20,44,69,1)","rgba(27,59,88,1)","rgba(20,46,71,1)","rgba(21,46,72,1)","rgba(20,46,71,1)","rgba(21,46,71,1)","rgba(19,43,67,1)","rgba(24,53,81,1)","rgba(21,46,72,1)","rgba(20,44,68,1)","rgba(20,45,70,1)","rgba(19,44,68,1)","rgba(19,44,68,1)","rgba(19,44,68,1)","rgba(25,55,83,1)","rgba(19,43,67,1)","rgba(20,46,71,1)","rgba(19,44,68,1)","rgba(19,43,67,1)","rgba(19,44,68,1)","rgba(22,48,74,1)","rgba(20,44,69,1)","rgba(22,49,75,1)","rgba(19,43,68,1)","rgba(19,43,67,1)","rgba(19,44,68,1)","rgba(20,44,69,1)","rgba(21,47,72,1)","rgba(19,43,67,1)","rgba(20,45,70,1)","rgba(19,43,68,1)","rgba(20,44,68,1)","rgba(39,83,120,1)","rgba(19,43,67,1)","rgba(19,43,67,1)","rgba(25,55,83,1)","rgba(27,59,89,1)","rgba(58,120,171,1)","rgba(20,45,70,1)","rgba(19,43,67,1)","rgba(20,45,70,1)","rgba(27,59,89,1)","rgba(31,67,99,1)","rgba(20,45,70,1)","rgba(24,53,81,1)","rgba(19,44,68,1)","rgba(25,55,83,1)","rgba(19,43,68,1)","rgba(24,53,80,1)","rgba(32,69,102,1)","rgba(20,44,69,1)","rgba(21,47,73,1)","rgba(20,45,69,1)","rgba(20,44,69,1)","rgba(22,50,76,1)","rgba(22,49,75,1)","rgba(21,46,71,1)","rgba(25,55,83,1)","rgba(29,62,93,1)"]}},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[38.8],"y":[-77.2],"name":"99_7d7836620f6f5117400b4f9346401503","type":"scatter","mode":"markers","opacity":0,"hoverinfo":"skip","showlegend":false,"marker":{"color":[0,1],"colorscale":[[0,"#132B43"],[0.00334448160535117,"#132B44"],[0.00668896321070234,"#132C44"],[0.0100334448160535,"#142C45"],[0.0133779264214047,"#142D45"],[0.0167224080267559,"#142D46"],[0.020066889632107,"#142D46"],[0.0234113712374582,"#142E47"],[0.0267558528428094,"#152E47"],[0.0301003344481605,"#152F48"],[0.0334448160535117,"#152F48"],[0.0367892976588629,"#152F49"],[0.040133779264214,"#153049"],[0.0434782608695652,"#16304A"],[0.0468227424749164,"#16304A"],[0.0501672240802676,"#16314B"],[0.0535117056856187,"#16314B"],[0.0568561872909699,"#16324C"],[0.0602006688963211,"#17324D"],[0.0635451505016722,"#17324D"],[0.0668896321070234,"#17334E"],[0.0702341137123746,"#17334E"],[0.0735785953177257,"#17344F"],[0.0769230769230769,"#18344F"],[0.0802675585284281,"#183450"],[0.0836120401337793,"#183550"],[0.0869565217391304,"#183551"],[0.0903010033444816,"#183651"],[0.0936454849498328,"#193652"],[0.0969899665551839,"#193652"],[0.100334448160535,"#193753"],[0.103678929765886,"#193754"],[0.107023411371237,"#193854"],[0.110367892976589,"#1A3855"],[0.11371237458194,"#1A3955"],[0.117056856187291,"#1A3956"],[0.120401337792642,"#1A3956"],[0.123745819397993,"#1A3A57"],[0.127090301003344,"#1B3A57"],[0.130434782608696,"#1B3B58"],[0.133779264214047,"#1B3B59"],[0.137123745819398,"#1B3B59"],[0.140468227424749,"#1C3C5A"],[0.1438127090301,"#1C3C5A"],[0.147157190635451,"#1C3D5B"],[0.150501672240803,"#1C3D5B"],[0.153846153846154,"#1C3D5C"],[0.157190635451505,"#1D3E5C"],[0.160535117056856,"#1D3E5D"],[0.163879598662207,"#1D3F5D"],[0.167224080267559,"#1D3F5E"],[0.17056856187291,"#1D3F5F"],[0.173913043478261,"#1E405F"],[0.177257525083612,"#1E4060"],[0.180602006688963,"#1E4160"],[0.183946488294314,"#1E4161"],[0.187290969899666,"#1E4261"],[0.190635451505017,"#1F4262"],[0.193979933110368,"#1F4263"],[0.197324414715719,"#1F4363"],[0.20066889632107,"#1F4364"],[0.204013377926421,"#1F4464"],[0.207357859531773,"#204465"],[0.210702341137124,"#204465"],[0.214046822742475,"#204566"],[0.217391304347826,"#204566"],[0.220735785953177,"#214667"],[0.224080267558528,"#214668"],[0.22742474916388,"#214768"],[0.230769230769231,"#214769"],[0.234113712374582,"#214769"],[0.237458193979933,"#22486A"],[0.240802675585284,"#22486A"],[0.244147157190635,"#22496B"],[0.247491638795987,"#22496C"],[0.250836120401338,"#224A6C"],[0.254180602006689,"#234A6D"],[0.25752508361204,"#234A6D"],[0.260869565217391,"#234B6E"],[0.264214046822742,"#234B6E"],[0.267558528428094,"#244C6F"],[0.270903010033445,"#244C70"],[0.274247491638796,"#244C70"],[0.277591973244147,"#244D71"],[0.280936454849498,"#244D71"],[0.284280936454849,"#254E72"],[0.287625418060201,"#254E72"],[0.290969899665552,"#254F73"],[0.294314381270903,"#254F74"],[0.297658862876254,"#254F74"],[0.301003344481605,"#265075"],[0.304347826086957,"#265075"],[0.307692307692308,"#265176"],[0.311036789297659,"#265176"],[0.31438127090301,"#275277"],[0.317725752508361,"#275278"],[0.321070234113712,"#275278"],[0.324414715719063,"#275379"],[0.327759197324415,"#275379"],[0.331103678929766,"#28547A"],[0.334448160535117,"#28547B"],[0.337792642140468,"#28557B"],[0.341137123745819,"#28557C"],[0.344481605351171,"#28567C"],[0.347826086956522,"#29567D"],[0.351170568561873,"#29567D"],[0.354515050167224,"#29577E"],[0.357859531772575,"#29577F"],[0.361204013377926,"#2A587F"],[0.364548494983278,"#2A5880"],[0.367892976588629,"#2A5980"],[0.37123745819398,"#2A5981"],[0.374581939799331,"#2A5982"],[0.377926421404682,"#2B5A82"],[0.381270903010033,"#2B5A83"],[0.384615384615385,"#2B5B83"],[0.387959866220736,"#2B5B84"],[0.391304347826087,"#2C5C85"],[0.394648829431438,"#2C5C85"],[0.397993311036789,"#2C5D86"],[0.40133779264214,"#2C5D86"],[0.404682274247492,"#2C5D87"],[0.408026755852843,"#2D5E87"],[0.411371237458194,"#2D5E88"],[0.414715719063545,"#2D5F89"],[0.418060200668896,"#2D5F89"],[0.421404682274247,"#2E608A"],[0.424749163879599,"#2E608A"],[0.42809364548495,"#2E618B"],[0.431438127090301,"#2E618C"],[0.434782608695652,"#2E618C"],[0.438127090301003,"#2F628D"],[0.441471571906354,"#2F628D"],[0.444816053511706,"#2F638E"],[0.448160535117057,"#2F638F"],[0.451505016722408,"#30648F"],[0.454849498327759,"#306490"],[0.45819397993311,"#306590"],[0.461538461538462,"#306591"],[0.464882943143813,"#306592"],[0.468227424749164,"#316692"],[0.471571906354515,"#316693"],[0.474916387959866,"#316793"],[0.478260869565217,"#316794"],[0.481605351170569,"#326895"],[0.48494983277592,"#326895"],[0.488294314381271,"#326996"],[0.491638795986622,"#326996"],[0.494983277591973,"#326997"],[0.498327759197324,"#336A98"],[0.501672240802676,"#336A98"],[0.505016722408027,"#336B99"],[0.508361204013378,"#336B99"],[0.511705685618729,"#346C9A"],[0.51505016722408,"#346C9B"],[0.518394648829431,"#346D9B"],[0.521739130434783,"#346D9C"],[0.525083612040134,"#346E9D"],[0.528428093645485,"#356E9D"],[0.531772575250836,"#356E9E"],[0.535117056856187,"#356F9E"],[0.538461538461538,"#356F9F"],[0.54180602006689,"#3670A0"],[0.545150501672241,"#3670A0"],[0.548494983277592,"#3671A1"],[0.551839464882943,"#3671A1"],[0.555183946488294,"#3772A2"],[0.558528428093645,"#3772A3"],[0.561872909698997,"#3773A3"],[0.565217391304348,"#3773A4"],[0.568561872909699,"#3773A4"],[0.57190635451505,"#3874A5"],[0.575250836120401,"#3874A6"],[0.578595317725753,"#3875A6"],[0.581939799331104,"#3875A7"],[0.585284280936455,"#3976A8"],[0.588628762541806,"#3976A8"],[0.591973244147157,"#3977A9"],[0.595317725752508,"#3977A9"],[0.598662207357859,"#3978AA"],[0.602006688963211,"#3A78AB"],[0.605351170568562,"#3A79AB"],[0.608695652173913,"#3A79AC"],[0.612040133779264,"#3A79AC"],[0.615384615384615,"#3B7AAD"],[0.618729096989966,"#3B7AAE"],[0.622073578595318,"#3B7BAE"],[0.625418060200669,"#3B7BAF"],[0.62876254180602,"#3C7CB0"],[0.632107023411371,"#3C7CB0"],[0.635451505016722,"#3C7DB1"],[0.638795986622073,"#3C7DB1"],[0.642140468227425,"#3C7EB2"],[0.645484949832776,"#3D7EB3"],[0.648829431438127,"#3D7FB3"],[0.652173913043478,"#3D7FB4"],[0.655518394648829,"#3D7FB5"],[0.658862876254181,"#3E80B5"],[0.662207357859532,"#3E80B6"],[0.665551839464883,"#3E81B6"],[0.668896321070234,"#3E81B7"],[0.672240802675585,"#3F82B8"],[0.675585284280936,"#3F82B8"],[0.678929765886288,"#3F83B9"],[0.682274247491639,"#3F83BA"],[0.68561872909699,"#4084BA"],[0.688963210702341,"#4084BB"],[0.692307692307692,"#4085BB"],[0.695652173913043,"#4085BC"],[0.698996655518395,"#4086BD"],[0.702341137123746,"#4186BD"],[0.705685618729097,"#4186BE"],[0.709030100334448,"#4187BF"],[0.712374581939799,"#4187BF"],[0.71571906354515,"#4288C0"],[0.719063545150502,"#4288C1"],[0.722408026755853,"#4289C1"],[0.725752508361204,"#4289C2"],[0.729096989966555,"#438AC2"],[0.732441471571906,"#438AC3"],[0.735785953177257,"#438BC4"],[0.739130434782609,"#438BC4"],[0.74247491638796,"#438CC5"],[0.745819397993311,"#448CC6"],[0.749163879598662,"#448DC6"],[0.752508361204013,"#448DC7"],[0.755852842809365,"#448EC8"],[0.759197324414716,"#458EC8"],[0.762541806020067,"#458FC9"],[0.765886287625418,"#458FC9"],[0.769230769230769,"#458FCA"],[0.77257525083612,"#4690CB"],[0.775919732441471,"#4690CB"],[0.779264214046823,"#4691CC"],[0.782608695652174,"#4691CD"],[0.785953177257525,"#4792CD"],[0.789297658862876,"#4792CE"],[0.792642140468227,"#4793CF"],[0.795986622073579,"#4793CF"],[0.79933110367893,"#4894D0"],[0.802675585284281,"#4894D0"],[0.806020066889632,"#4895D1"],[0.809364548494983,"#4895D2"],[0.812709030100334,"#4896D2"],[0.816053511705686,"#4996D3"],[0.819397993311037,"#4997D4"],[0.822742474916388,"#4997D4"],[0.826086956521739,"#4998D5"],[0.82943143812709,"#4A98D6"],[0.832775919732441,"#4A99D6"],[0.836120401337793,"#4A99D7"],[0.839464882943144,"#4A9AD8"],[0.842809364548495,"#4B9AD8"],[0.846153846153846,"#4B9BD9"],[0.849498327759197,"#4B9BDA"],[0.852842809364548,"#4B9BDA"],[0.8561872909699,"#4C9CDB"],[0.859531772575251,"#4C9CDB"],[0.862876254180602,"#4C9DDC"],[0.866220735785953,"#4C9DDD"],[0.869565217391304,"#4D9EDD"],[0.872909698996655,"#4D9EDE"],[0.876254180602007,"#4D9FDF"],[0.879598662207358,"#4D9FDF"],[0.882943143812709,"#4DA0E0"],[0.88628762541806,"#4EA0E1"],[0.889632107023411,"#4EA1E1"],[0.892976588628763,"#4EA1E2"],[0.896321070234114,"#4EA2E3"],[0.899665551839465,"#4FA2E3"],[0.903010033444816,"#4FA3E4"],[0.906354515050167,"#4FA3E5"],[0.909698996655518,"#4FA4E5"],[0.91304347826087,"#50A4E6"],[0.916387959866221,"#50A5E7"],[0.919732441471572,"#50A5E7"],[0.923076923076923,"#50A6E8"],[0.926421404682274,"#51A6E8"],[0.929765886287625,"#51A7E9"],[0.933110367892977,"#51A7EA"],[0.936454849498328,"#51A8EA"],[0.939799331103679,"#52A8EB"],[0.94314381270903,"#52A9EC"],[0.946488294314381,"#52A9EC"],[0.949832775919732,"#52AAED"],[0.953177257525084,"#53AAEE"],[0.956521739130435,"#53ABEE"],[0.959866220735786,"#53ABEF"],[0.963210702341137,"#53ACF0"],[0.966555183946488,"#54ACF0"],[0.969899665551839,"#54ADF1"],[0.973244147157191,"#54ADF2"],[0.976588628762542,"#54AEF2"],[0.979933110367893,"#55AEF3"],[0.983277591973244,"#55AFF4"],[0.986622073578595,"#55AFF4"],[0.989966555183946,"#55B0F5"],[0.993311036789298,"#56B0F6"],[0.996655518394649,"#56B1F6"],[1,"#56B1F7"]],"colorbar":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"thickness":23.04,"title":"num_departures","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"tickmode":"array","ticktext":["4000","8000","12000"],"tickvals":[0.251858384780144,0.503842761748772,0.755827138717399],"tickfont":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"ticklen":2,"len":0.5}},"xaxis":"x","yaxis":"y","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":40.1826484018265,"l":54.7945205479452},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Map of Stations based on Longitude and Latitude Positioning","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[38.7849909,39.1396331],"tickmode":"array","ticktext":["38.8","38.9","39.0","39.1"],"tickvals":[38.8,38.9,39,39.1],"categoryorder":"array","categoryarray":["38.8","38.9","39.0","39.1"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"Longitude","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-77.21603295,-76.91833005],"tickmode":"array","ticktext":["-77.2","-77.1","-77.0"],"tickvals":[-77.2,-77.1,-77],"categoryorder":"array","categoryarray":["-77.2","-77.1","-77.0"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"Latitude","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"32cbee4fc1f":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"32cbee4fc1f","visdat":{"32cbee4fc1f":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```
  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).

Month 4: Paris Nord station has a sliver of a different color at the end! Why?


```r
num_trips_depart <- small_trains %>% 
  select(year, month, service, departure_station, total_num_trips) %>% 
  filter(year == 2016,
         service == "National",
         departure_station %in% c("MARSEILLE ST CHARLES", "LILLE", "PARIS NORD", "TOURS", "RENNES", "PARIS EST")) %>%
  group_by(departure_station, month) %>% 
  mutate(total_num_trips = sum(total_num_trips)) %>% 
  distinct() %>% 
  ggplot(aes(x = total_num_trips, y = reorder(departure_station, total_num_trips)))+
  geom_col(aes(fill = total_num_trips))+
  labs(title = "Number of Trips from Departure Stations",
       subtitle = "Year: 2016, Month: {closest_state}",
       x = "Number of Trips",
       y = "")+
  theme(legend.position = "none")+
  scale_fill_viridis_c(option = "plasma")+
  transition_states(month)

anim_save("num_trips_depart.gif",
          animation = num_trips_depart)
```



```r
knitr::include_graphics("num_trips_depart.gif")
```

<img src="num_trips_depart.gif" title="Animated Graph that shows the number of trips from certain departure stations in France. The animation shows the different months of 2016, the bars are colored by number of trips which the Paris Nord and Paris Est stations having the largest values of roughly 8000." alt="Animated Graph that shows the number of trips from certain departure stations in France. The animation shows the different months of 2016, the bars are colored by number of trips which the Paris Nord and Paris Est stations having the largest values of roughly 8000."  />

## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. I have filtered the data to the tomatoes and find the *daily* harvest in pounds for each variety. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0. 
  You should do the following:
  * For each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each variety and arranged (HINT: `fct_reorder()`) from most to least harvested weights (most on the bottom).  
  * Add animation to reveal the plot over date. Instead of having a legend, place the variety names directly on the graph (refer back to the tutorial for how to do this).


```r
tomato_cumsum_graph <- garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  ungroup() %>% 
  complete(variety, 
           date, 
           fill = list(daily_harvest_lb = 0)) %>% 
  group_by(variety) %>% 
  mutate(cum_harvest_lb = cumsum(daily_harvest_lb)) %>% 
  ggplot(aes(x=date, y=cum_harvest_lb, fill = fct_reorder(variety, cum_harvest_lb, max)))+
  geom_area()+
  geom_text(aes(label = variety), position = "stack") +
  transition_reveal(date)+
  theme(legend.position = "none")
  
anim_save("tomato_cumsum_graph.gif",
          animation = tomato_cumsum_graph)
```



```r
knitr::include_graphics("tomato_cumsum_graph.gif")
```

<img src="tomato_cumsum_graph.gif"  />

## Maps, animation, and movement!

  4. Map Lisa's `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example.
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  
  ADD SOMETHING OF MY OWN
  
I prefer this map to not be static because I like seeing the way that the timing affects how the map is drawn, it makes it more realistic and shows the time in a way that would not be possible with a static map. It would be possible to color by speed but then elevation would not be accounted for.


```r
mallorca_map <- get_stamenmap(
    bbox = c(left = 2.3084, bottom = 39.5448, right = 2.6826, top = 39.7156),
    maptype = "terrain",
    zoom = 12)

anim_biking_mallorca <- ggmap(mallorca_map)+
  geom_point(data = mallorca_bike_day7,
            aes(x = lon, y = lat),
            color = "red",
            size = 1.2) +
  geom_path(data = mallorca_bike_day7, 
             aes(x = lon, y = lat, color = ele),
             size = 1) +
  scale_color_viridis_c("Elevation", option = "plasma") +
  labs(title = "Map of Biking Data in Mallorca",
       subtitle = "Time : {frame_along}",
       x = "",
       y = "")+
  theme_map() +
  theme(legend.background = element_blank(),
        legend.position = c(0.02, 0.6)) +
  transition_reveal(time)

anim_save("anim_biking_mallorca.gif",
          animation = anim_biking_mallorca)
```
  
  

```r
knitr::include_graphics("anim_biking_mallorca.gif")
```

<img src="anim_biking_mallorca.gif" title="An animated map that shows a path taken around Western Mallorca by bike with the path colored by elevation." alt="An animated map that shows a path taken around Western Mallorca by bike with the path colored by elevation."  />
  
  5. In this exercise, you get to meet Lisa's sister, Heather! She is a proud Mac grad, currently works as a Data Scientist where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files putting them in swim, bike, run order (HINT: `bind_rows()`), 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

```r
swim_bike_run <- panama_swim %>% 
  bind_rows(panama_bike, panama_run)

panama_map <- get_stamenmap(
    bbox = c(left = -79.6022, bottom = 8.9007, right = -79.4550, top = 9.0102),
    maptype = "terrain",
    zoom = 13)

ironman_map <- ggmap(panama_map)+
  geom_point(data = swim_bike_run,
            aes(x = lon, y = lat, color = event),
            size = 1.5) +
  geom_path(data = swim_bike_run, 
             aes(x = lon, y = lat, color = event),
             size = .8) +
  scale_color_viridis_d("Event", option = "plasma") +
  labs(title = "Map of Ironman 70.3 Pan Am in Panama",
       subtitle = "Time : {frame_along}",
       x = "",
       y = "")+
  theme_map()+
  theme(legend.background = element_blank(),
        legend.position = c(0.86, 0.1)) +
  transition_reveal(time)

anim_save("ironman_map.gif",
          animation = ironman_map)
```
  

```r
knitr::include_graphics("ironman_map.gif")
```

<img src="ironman_map.gif"  />
  
## COVID-19 data

  6. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for the the 15th of each month. So, filter only to those dates - there are some lubridate functions that can help you do this.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  
  
The map only shows some of the states in the first 2 months, this is because there were no Covid-19 cases recorded in those states yet. However as time goes on all the states show up and then they are colored based on the number of cumulative cases for the state. The states with the highest population, New York and California, had a much larger number of cases compared to the rest of the country.


```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))

states_map <- map_data("state")

cum_covid <- covid19 %>% 
  group_by(`state`, `date`) %>% 
  mutate(state = str_to_lower(`state`),
         day_of_month = day(date)) %>% 
  filter(day_of_month == 15 ) %>% 
  distinct() %>% 
  ungroup()

covid_map <- cum_covid %>% 
  ggplot()+
  geom_map(map = states_map,
            aes(map_id = state,
                fill = cases,
                group = date)) +
  scale_fill_distiller(type = "div", palette = "PuBuGn")+
  expand_limits(x = states_map$long, y = states_map$lat)+
  theme_map()+
  labs(title = "Cumulative Number of COVID-19 Cases by State",
       subtitle = "Date: {closest_state}")+
  theme(plot.title = element_text(hjust = 0.5),
        plot.subtitle = element_text(hjust = 0.5))+
  transition_states(date)

anim_covid_map <- animate(covid_map, nframes = 200, end_pause = 10)

anim_save("anim_covid_map.gif",
          animation = anim_covid_map)
```


```r
knitr::include_graphics("anim_covid_map.gif")
```

<img src="anim_covid_map.gif"  />


## Your first `shiny` app

  7. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. You should create a new project for the app, separate from the homework project. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' daily number of COVID cases per 100,000 over time. The x-axis will be date. You will have an input box where the user can choose which states to compare (`selectInput()`), a slider where the user can choose the date range, and a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
Put the link to your app here: 
  
## GitHub link

  8. Below, provide a link to your GitHub repo with this set of Weekly Exercises. 


**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
