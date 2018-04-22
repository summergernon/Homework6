
Observed trend 1: The max temperature increases the closer you get to the equater.
Observed trend 2: Wind speed does not seem to be correlated with latitude.
Observed trend 3: It appears that it is less humid north of the equator compared to south of the equator.


```python
# Dependencies
from citipy import citipy
from random import uniform 
import pandas as pd
from config import api_key
import requests
import numpy as np
import matplotlib.pyplot as plt
import csv

```


```python
# Create empty lists
cities = []
coordinates = []

for x in range(1,1200):
    # Pick a random value between -90 and 90 for the lat and lng and round it to 2 decimal places
    lat = round(uniform(-90,90),2)
    lng = round(uniform(-180,180),2)
    coords = (lat, lng)
    coordinates.append(coords)
    # Find nearest city to our random coordinates
    city = citipy.nearest_city(lat, lng)
    city_name = city.city_name
    cities.append(city_name)


```


```python
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "imperial"

query_url = f"{url}appid={api_key}&units={units}&q="
```


```python
# Create empty lists to store information about each city
temp = []
humidity = []
cloudiness = []
wind_speed = []
valid_cities = []
valid_lat = []

# Loop through the list of cities and perform a request for data on each
# If the city does not have the information below, it will print not found
for city in cities:
    try: 
        response = requests.get(query_url+ city).json()
        temp.append(response['main']['temp_max'])
        humidity.append(response['main']['humidity'])
        cloudiness.append(response['clouds']['all'])
        wind_speed.append(response['wind']['speed'])
        valid_lat.append(response['coord']['lat'])
        valid_cities.append(city)
    except:
        print(f'{city} not found')
        continue
```

    nizhneyansk not found
    belushya guba not found
    ciras not found
    ondorhaan not found
    bardiyah not found
    vaitupu not found
    taolanaro not found
    tsihombe not found
    taolanaro not found
    sentyabrskiy not found
    himora not found
    boatlaname not found
    barentsburg not found
    taolanaro not found
    taolanaro not found
    attawapiskat not found
    tungkang not found
    tawkar not found
    irbil not found
    attawapiskat not found
    asau not found
    bengkulu not found
    amderma not found
    grand river south east not found
    illoqqortoormiut not found
    dianopolis not found
    mergui not found
    nizhneyansk not found
    barentsburg not found
    nizhneyansk not found
    bengkulu not found
    amderma not found
    belushya guba not found
    bengkulu not found
    belushya guba not found
    cumaribo not found
    mullaitivu not found
    illoqqortoormiut not found
    pemangkat not found
    mys shmidta not found
    amderma not found
    asau not found
    taolanaro not found
    meyungs not found
    ituni not found
    riaba not found
    rungata not found
    taolanaro not found
    asfi not found
    taolanaro not found
    taolanaro not found
    tumannyy not found
    kashi not found
    amderma not found
    kazalinsk not found
    taolanaro not found
    taolanaro not found
    saleaula not found
    houlung not found
    litoral del san juan not found
    zachagansk not found
    barentsburg not found
    aflu not found
    asfi not found
    krasnoselkup not found
    shcholkine not found
    kapoeta not found
    taolanaro not found
    bengkulu not found
    obluche not found
    taolanaro not found
    hunza not found
    amderma not found
    gardan diwal not found
    mataura not found
    umzimvubu not found
    tekax not found
    barawe not found
    wulanhaote not found
    bengkulu not found
    parras not found
    grand river south east not found
    vaitupu not found
    taolanaro not found
    nizhneyansk not found
    karaul not found
    lolua not found
    taolanaro not found
    samusu not found
    taolanaro not found
    attawapiskat not found
    taolanaro not found
    samusu not found
    jibuti not found
    taolanaro not found
    barentsburg not found
    krasnoselkup not found
    stornoway not found
    armacao dos buzios not found
    taolanaro not found
    illoqqortoormiut not found
    olafsvik not found
    a not found
    mys shmidta not found
    amderma not found
    huetamo not found
    illoqqortoormiut not found
    illoqqortoormiut not found
    belushya guba not found
    satitoa not found
    bengkulu not found
    sentyabrskiy not found
    qandahar not found
    bolungarvik not found
    nizhneyansk not found
    belushya guba not found
    taolanaro not found
    barentsburg not found
    taolanaro not found
    formoso do araguaia not found
    amderma not found
    stoyba not found
    illoqqortoormiut not found
    kyra not found
    januaria not found



```python
# Confirm that we have at least 500 cities
len(valid_cities)
```




    1074




```python
# Print out log
print(f"Beginning Data Retrieval")
print(f"-----------------------------")
counter = 1
for city in valid_cities:
    print(f"Processing Record {counter} for {city}")
    print(query_url + city)
    counter += 1
print(f"-----------------------------")
print(f"Data Retrieval Complete")
print(f"-----------------------------")
```

    Beginning Data Retrieval
    -----------------------------
    Processing Record 1 for laguna
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=laguna
    Processing Record 2 for kaitangata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kaitangata
    Processing Record 3 for hobyo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobyo
    Processing Record 4 for christchurch
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=christchurch
    Processing Record 5 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 6 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 7 for karratha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=karratha
    Processing Record 8 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 9 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 10 for saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saskylakh
    Processing Record 11 for yerofey pavlovich
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yerofey pavlovich
    Processing Record 12 for tiksi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tiksi
    Processing Record 13 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 14 for los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=los llanos de aridane
    Processing Record 15 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 16 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 17 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 18 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 19 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 20 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 21 for kavieng
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kavieng
    Processing Record 22 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 23 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 24 for vuktyl
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vuktyl
    Processing Record 25 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 26 for oksfjord
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=oksfjord
    Processing Record 27 for dikson
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=dikson
    Processing Record 28 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 29 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 30 for maragogi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=maragogi
    Processing Record 31 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 32 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 33 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 34 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 35 for bow island
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bow island
    Processing Record 36 for juba
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=juba
    Processing Record 37 for khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khatanga
    Processing Record 38 for bubanza
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bubanza
    Processing Record 39 for carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=carnarvon
    Processing Record 40 for ilulissat
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ilulissat
    Processing Record 41 for bereda
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bereda
    Processing Record 42 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 43 for bethel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bethel
    Processing Record 44 for fortuna
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=fortuna
    Processing Record 45 for puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto ayora
    Processing Record 46 for xining
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=xining
    Processing Record 47 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 48 for poum
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=poum
    Processing Record 49 for victoria
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=victoria
    Processing Record 50 for pevek
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pevek
    Processing Record 51 for airai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=airai
    Processing Record 52 for ranong
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ranong
    Processing Record 53 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 54 for aykhal
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=aykhal
    Processing Record 55 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 56 for verkhoshizhemye
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=verkhoshizhemye
    Processing Record 57 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 58 for bethel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bethel
    Processing Record 59 for golfito
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=golfito
    Processing Record 60 for ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ostrovnoy
    Processing Record 61 for henties bay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=henties bay
    Processing Record 62 for guerrero negro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=guerrero negro
    Processing Record 63 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 64 for payson
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=payson
    Processing Record 65 for bethel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bethel
    Processing Record 66 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 67 for puerto del rosario
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto del rosario
    Processing Record 68 for khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khatanga
    Processing Record 69 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 70 for alofi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=alofi
    Processing Record 71 for ruteng
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ruteng
    Processing Record 72 for moose factory
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=moose factory
    Processing Record 73 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 74 for kavieng
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kavieng
    Processing Record 75 for arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arraial do cabo
    Processing Record 76 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 77 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 78 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 79 for pemba
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pemba
    Processing Record 80 for souillac
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=souillac
    Processing Record 81 for arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arraial do cabo
    Processing Record 82 for saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saskylakh
    Processing Record 83 for victoria
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=victoria
    Processing Record 84 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 85 for sorland
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sorland
    Processing Record 86 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 87 for horodnytsya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=horodnytsya
    Processing Record 88 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 89 for muros
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=muros
    Processing Record 90 for cody
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cody
    Processing Record 91 for gokak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=gokak
    Processing Record 92 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 93 for beringovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=beringovskiy
    Processing Record 94 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 95 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 96 for amapa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=amapa
    Processing Record 97 for haines junction
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=haines junction
    Processing Record 98 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 99 for husum
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=husum
    Processing Record 100 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 101 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 102 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 103 for geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=geraldton
    Processing Record 104 for khani
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khani
    Processing Record 105 for longyearbyen
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=longyearbyen
    Processing Record 106 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 107 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 108 for sechura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sechura
    Processing Record 109 for thompson
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=thompson
    Processing Record 110 for penal
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=penal
    Processing Record 111 for sao joao da barra
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sao joao da barra
    Processing Record 112 for tiksi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tiksi
    Processing Record 113 for sitka
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sitka
    Processing Record 114 for matagami
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=matagami
    Processing Record 115 for nanortalik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nanortalik
    Processing Record 116 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 117 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 118 for qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=qaanaaq
    Processing Record 119 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 120 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 121 for lebu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lebu
    Processing Record 122 for qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=qaanaaq
    Processing Record 123 for luderitz
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=luderitz
    Processing Record 124 for ambilobe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ambilobe
    Processing Record 125 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 126 for yulara
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yulara
    Processing Record 127 for mpulungu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mpulungu
    Processing Record 128 for yar-sale
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yar-sale
    Processing Record 129 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 130 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 131 for banyo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=banyo
    Processing Record 132 for bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bambous virieux
    Processing Record 133 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 134 for khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khatanga
    Processing Record 135 for atambua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atambua
    Processing Record 136 for champerico
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=champerico
    Processing Record 137 for saint-pierre
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saint-pierre
    Processing Record 138 for tasiilaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tasiilaq
    Processing Record 139 for haapiti
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=haapiti
    Processing Record 140 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 141 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 142 for arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arraial do cabo
    Processing Record 143 for saint-philippe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saint-philippe
    Processing Record 144 for karratha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=karratha
    Processing Record 145 for carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=carnarvon
    Processing Record 146 for mount gambier
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mount gambier
    Processing Record 147 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 148 for arman
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arman
    Processing Record 149 for drochtersen
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=drochtersen
    Processing Record 150 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 151 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 152 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 153 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 154 for enshi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=enshi
    Processing Record 155 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 156 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 157 for yelnya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yelnya
    Processing Record 158 for avarua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=avarua
    Processing Record 159 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 160 for lorengau
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lorengau
    Processing Record 161 for tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tuktoyaktuk
    Processing Record 162 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 163 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 164 for bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bathsheba
    Processing Record 165 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 166 for lebu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lebu
    Processing Record 167 for lethem
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lethem
    Processing Record 168 for tabuk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tabuk
    Processing Record 169 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 170 for vredefort
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vredefort
    Processing Record 171 for tangzhai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tangzhai
    Processing Record 172 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 173 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 174 for madaoua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=madaoua
    Processing Record 175 for lorengau
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lorengau
    Processing Record 176 for mangrol
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mangrol
    Processing Record 177 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 178 for carmo do rio claro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=carmo do rio claro
    Processing Record 179 for saint anthony
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saint anthony
    Processing Record 180 for harper
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=harper
    Processing Record 181 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 182 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 183 for derbent
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=derbent
    Processing Record 184 for the valley
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=the valley
    Processing Record 185 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 186 for grand gaube
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=grand gaube
    Processing Record 187 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 188 for kindu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kindu
    Processing Record 189 for upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=upernavik
    Processing Record 190 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 191 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 192 for outlook
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=outlook
    Processing Record 193 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 194 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 195 for los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=los llanos de aridane
    Processing Record 196 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 197 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 198 for ishurdi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ishurdi
    Processing Record 199 for ilulissat
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ilulissat
    Processing Record 200 for conde
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=conde
    Processing Record 201 for yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yellowknife
    Processing Record 202 for nabire
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nabire
    Processing Record 203 for ngunguru
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ngunguru
    Processing Record 204 for souris
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=souris
    Processing Record 205 for belfast
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=belfast
    Processing Record 206 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 207 for mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mahebourg
    Processing Record 208 for bilibino
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bilibino
    Processing Record 209 for pisco
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pisco
    Processing Record 210 for praia da vitoria
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=praia da vitoria
    Processing Record 211 for ancud
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ancud
    Processing Record 212 for nouadhibou
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nouadhibou
    Processing Record 213 for carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=carnarvon
    Processing Record 214 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 215 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 216 for igarka
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=igarka
    Processing Record 217 for watrous
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=watrous
    Processing Record 218 for along
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=along
    Processing Record 219 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 220 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 221 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 222 for sachica
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sachica
    Processing Record 223 for mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mahebourg
    Processing Record 224 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 225 for ahipara
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ahipara
    Processing Record 226 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 227 for hay river
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hay river
    Processing Record 228 for bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bredasdorp
    Processing Record 229 for husavik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=husavik
    Processing Record 230 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 231 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 232 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 233 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 234 for aklavik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=aklavik
    Processing Record 235 for sao geraldo do araguaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sao geraldo do araguaia
    Processing Record 236 for santa rosa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=santa rosa
    Processing Record 237 for puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto ayora
    Processing Record 238 for nyurba
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nyurba
    Processing Record 239 for puerto baquerizo moreno
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto baquerizo moreno
    Processing Record 240 for lata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lata
    Processing Record 241 for puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto ayora
    Processing Record 242 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 243 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 244 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 245 for leshukonskoye
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=leshukonskoye
    Processing Record 246 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 247 for caravelas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=caravelas
    Processing Record 248 for namatanai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=namatanai
    Processing Record 249 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 250 for bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bredasdorp
    Processing Record 251 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 252 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 253 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 254 for yurga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yurga
    Processing Record 255 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 256 for westport
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=westport
    Processing Record 257 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 258 for aksu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=aksu
    Processing Record 259 for acapulco
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=acapulco
    Processing Record 260 for ilulissat
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ilulissat
    Processing Record 261 for ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ribeira grande
    Processing Record 262 for la joya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=la joya
    Processing Record 263 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 264 for bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bambous virieux
    Processing Record 265 for basco
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=basco
    Processing Record 266 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 267 for maine-soroa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=maine-soroa
    Processing Record 268 for gao
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=gao
    Processing Record 269 for nikolskoye
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nikolskoye
    Processing Record 270 for luganville
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=luganville
    Processing Record 271 for san ramon de la nueva oran
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=san ramon de la nueva oran
    Processing Record 272 for shenjiamen
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=shenjiamen
    Processing Record 273 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 274 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 275 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 276 for zhangye
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=zhangye
    Processing Record 277 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 278 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 279 for provideniya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=provideniya
    Processing Record 280 for nuuk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nuuk
    Processing Record 281 for longyearbyen
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=longyearbyen
    Processing Record 282 for beira
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=beira
    Processing Record 283 for namibe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=namibe
    Processing Record 284 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 285 for saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saskylakh
    Processing Record 286 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 287 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 288 for sciacca
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sciacca
    Processing Record 289 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 290 for bethel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bethel
    Processing Record 291 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 292 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 293 for mayor pablo lagerenza
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mayor pablo lagerenza
    Processing Record 294 for tasiilaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tasiilaq
    Processing Record 295 for biltine
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=biltine
    Processing Record 296 for mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mahebourg
    Processing Record 297 for maua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=maua
    Processing Record 298 for bud
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bud
    Processing Record 299 for esperance
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=esperance
    Processing Record 300 for ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ribeira grande
    Processing Record 301 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 302 for georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=georgetown
    Processing Record 303 for ilulissat
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ilulissat
    Processing Record 304 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 305 for puerto escondido
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto escondido
    Processing Record 306 for bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bathsheba
    Processing Record 307 for beroroha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=beroroha
    Processing Record 308 for hithadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hithadhoo
    Processing Record 309 for longyearbyen
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=longyearbyen
    Processing Record 310 for airai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=airai
    Processing Record 311 for wiang sa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=wiang sa
    Processing Record 312 for elban
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=elban
    Processing Record 313 for bethel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bethel
    Processing Record 314 for warmbad
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=warmbad
    Processing Record 315 for hauterive
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hauterive
    Processing Record 316 for phan thiet
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=phan thiet
    Processing Record 317 for maturin
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=maturin
    Processing Record 318 for torbay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=torbay
    Processing Record 319 for kawalu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kawalu
    Processing Record 320 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 321 for naze
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=naze
    Processing Record 322 for singaparna
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=singaparna
    Processing Record 323 for yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yellowknife
    Processing Record 324 for yumen
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yumen
    Processing Record 325 for cravo norte
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cravo norte
    Processing Record 326 for iberia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=iberia
    Processing Record 327 for iqaluit
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=iqaluit
    Processing Record 328 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 329 for hobyo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobyo
    Processing Record 330 for mount gambier
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mount gambier
    Processing Record 331 for lavrentiya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lavrentiya
    Processing Record 332 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 333 for tasiilaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tasiilaq
    Processing Record 334 for upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=upernavik
    Processing Record 335 for tezu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tezu
    Processing Record 336 for faanui
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=faanui
    Processing Record 337 for inhambane
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=inhambane
    Processing Record 338 for luderitz
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=luderitz
    Processing Record 339 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 340 for hoa binh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hoa binh
    Processing Record 341 for vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vestmannaeyjar
    Processing Record 342 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 343 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 344 for puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto ayora
    Processing Record 345 for tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tuktoyaktuk
    Processing Record 346 for bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bambous virieux
    Processing Record 347 for karwar
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=karwar
    Processing Record 348 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 349 for port said
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port said
    Processing Record 350 for mantua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mantua
    Processing Record 351 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 352 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 353 for tual
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tual
    Processing Record 354 for cadillac
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cadillac
    Processing Record 355 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 356 for qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=qaanaaq
    Processing Record 357 for ayan
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ayan
    Processing Record 358 for bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bambous virieux
    Processing Record 359 for clyde river
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=clyde river
    Processing Record 360 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 361 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 362 for bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bambous virieux
    Processing Record 363 for la baule-escoublac
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=la baule-escoublac
    Processing Record 364 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 365 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 366 for chara
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=chara
    Processing Record 367 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 368 for estelle
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=estelle
    Processing Record 369 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 370 for ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ribeira grande
    Processing Record 371 for khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khatanga
    Processing Record 372 for puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto ayora
    Processing Record 373 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 374 for zvishavane
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=zvishavane
    Processing Record 375 for iqaluit
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=iqaluit
    Processing Record 376 for kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodiak
    Processing Record 377 for kodinar
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodinar
    Processing Record 378 for buin
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=buin
    Processing Record 379 for leningradskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=leningradskiy
    Processing Record 380 for grenville
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=grenville
    Processing Record 381 for geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=geraldton
    Processing Record 382 for mount gambier
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mount gambier
    Processing Record 383 for havelock
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=havelock
    Processing Record 384 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 385 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 386 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 387 for marsberg
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=marsberg
    Processing Record 388 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 389 for matay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=matay
    Processing Record 390 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 391 for gotsu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=gotsu
    Processing Record 392 for kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodiak
    Processing Record 393 for bodden town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bodden town
    Processing Record 394 for bonnyville
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bonnyville
    Processing Record 395 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 396 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 397 for nanortalik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nanortalik
    Processing Record 398 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 399 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 400 for chimbote
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=chimbote
    Processing Record 401 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 402 for vila
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vila
    Processing Record 403 for pevek
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pevek
    Processing Record 404 for talcahuano
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=talcahuano
    Processing Record 405 for cayenne
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cayenne
    Processing Record 406 for qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=qaanaaq
    Processing Record 407 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 408 for ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ribeira grande
    Processing Record 409 for lebu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lebu
    Processing Record 410 for esso
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=esso
    Processing Record 411 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 412 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 413 for tongzi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tongzi
    Processing Record 414 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 415 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 416 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 417 for geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=geraldton
    Processing Record 418 for lagoa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lagoa
    Processing Record 419 for valleyview
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=valleyview
    Processing Record 420 for rio gallegos
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rio gallegos
    Processing Record 421 for guerrero negro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=guerrero negro
    Processing Record 422 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 423 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 424 for pisco
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pisco
    Processing Record 425 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 426 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 427 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 428 for provideniya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=provideniya
    Processing Record 429 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 430 for east london
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=east london
    Processing Record 431 for puerto baquerizo moreno
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto baquerizo moreno
    Processing Record 432 for vao
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vao
    Processing Record 433 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 434 for namatanai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=namatanai
    Processing Record 435 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 436 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 437 for sterling
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sterling
    Processing Record 438 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 439 for buraydah
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=buraydah
    Processing Record 440 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 441 for leningradskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=leningradskiy
    Processing Record 442 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 443 for nieves
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nieves
    Processing Record 444 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 445 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 446 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 447 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 448 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 449 for omboue
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=omboue
    Processing Record 450 for san pedro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=san pedro
    Processing Record 451 for qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=qaanaaq
    Processing Record 452 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 453 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 454 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 455 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 456 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 457 for bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bredasdorp
    Processing Record 458 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 459 for longyearbyen
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=longyearbyen
    Processing Record 460 for lavrentiya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lavrentiya
    Processing Record 461 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 462 for deputatskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=deputatskiy
    Processing Record 463 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 464 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 465 for saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saskylakh
    Processing Record 466 for sao gabriel da cachoeira
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sao gabriel da cachoeira
    Processing Record 467 for victoria
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=victoria
    Processing Record 468 for yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yellowknife
    Processing Record 469 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 470 for pacific grove
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pacific grove
    Processing Record 471 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 472 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 473 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 474 for adrar
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=adrar
    Processing Record 475 for antalaha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=antalaha
    Processing Record 476 for shieli
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=shieli
    Processing Record 477 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 478 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 479 for kruisfontein
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kruisfontein
    Processing Record 480 for bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bredasdorp
    Processing Record 481 for hamilton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hamilton
    Processing Record 482 for puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto ayora
    Processing Record 483 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 484 for salinopolis
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=salinopolis
    Processing Record 485 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 486 for la paz
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=la paz
    Processing Record 487 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 488 for bethel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bethel
    Processing Record 489 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 490 for buraydah
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=buraydah
    Processing Record 491 for nemuro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nemuro
    Processing Record 492 for tiksi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tiksi
    Processing Record 493 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 494 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 495 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 496 for arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arraial do cabo
    Processing Record 497 for sorong
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sorong
    Processing Record 498 for kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodiak
    Processing Record 499 for yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yellowknife
    Processing Record 500 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 501 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 502 for fuling
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=fuling
    Processing Record 503 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 504 for pangnirtung
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pangnirtung
    Processing Record 505 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 506 for dubti
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=dubti
    Processing Record 507 for havelock
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=havelock
    Processing Record 508 for kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodiak
    Processing Record 509 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 510 for ballitoville
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ballitoville
    Processing Record 511 for saurimo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saurimo
    Processing Record 512 for cherskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cherskiy
    Processing Record 513 for richards bay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=richards bay
    Processing Record 514 for tshikapa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tshikapa
    Processing Record 515 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 516 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 517 for faya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=faya
    Processing Record 518 for lucapa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lucapa
    Processing Record 519 for komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=komsomolskiy
    Processing Record 520 for evensk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=evensk
    Processing Record 521 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 522 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 523 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 524 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 525 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 526 for saint george
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saint george
    Processing Record 527 for batemans bay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=batemans bay
    Processing Record 528 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 529 for esperance
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=esperance
    Processing Record 530 for georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=georgetown
    Processing Record 531 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 532 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 533 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 534 for tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tuktoyaktuk
    Processing Record 535 for mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mahebourg
    Processing Record 536 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 537 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 538 for jieshi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jieshi
    Processing Record 539 for rio grande
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rio grande
    Processing Record 540 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 541 for leningradskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=leningradskiy
    Processing Record 542 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 543 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 544 for tasiilaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tasiilaq
    Processing Record 545 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 546 for abrau-dyurso
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=abrau-dyurso
    Processing Record 547 for buraydah
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=buraydah
    Processing Record 548 for nanortalik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nanortalik
    Processing Record 549 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 550 for maniwaki
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=maniwaki
    Processing Record 551 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 552 for baracoa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=baracoa
    Processing Record 553 for bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bathsheba
    Processing Record 554 for lebu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lebu
    Processing Record 555 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 556 for east london
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=east london
    Processing Record 557 for meihekou
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=meihekou
    Processing Record 558 for fare
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=fare
    Processing Record 559 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 560 for bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bredasdorp
    Processing Record 561 for gazli
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=gazli
    Processing Record 562 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 563 for airai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=airai
    Processing Record 564 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 565 for airai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=airai
    Processing Record 566 for sao joao da barra
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sao joao da barra
    Processing Record 567 for bethel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bethel
    Processing Record 568 for hamilton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hamilton
    Processing Record 569 for san jeronimo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=san jeronimo
    Processing Record 570 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 571 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 572 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 573 for roma
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=roma
    Processing Record 574 for kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodiak
    Processing Record 575 for saldanha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saldanha
    Processing Record 576 for havelock
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=havelock
    Processing Record 577 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 578 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 579 for cape canaveral
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape canaveral
    Processing Record 580 for takoradi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=takoradi
    Processing Record 581 for zeerust
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=zeerust
    Processing Record 582 for kavieng
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kavieng
    Processing Record 583 for torbay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=torbay
    Processing Record 584 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 585 for olinda
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=olinda
    Processing Record 586 for atambua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atambua
    Processing Record 587 for kavieng
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kavieng
    Processing Record 588 for nanortalik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nanortalik
    Processing Record 589 for qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=qaanaaq
    Processing Record 590 for marystown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=marystown
    Processing Record 591 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 592 for seoul
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=seoul
    Processing Record 593 for champasak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=champasak
    Processing Record 594 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 595 for vostok
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vostok
    Processing Record 596 for arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arraial do cabo
    Processing Record 597 for taloqan
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=taloqan
    Processing Record 598 for ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ribeira grande
    Processing Record 599 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 600 for luderitz
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=luderitz
    Processing Record 601 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 602 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 603 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 604 for geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=geraldton
    Processing Record 605 for polunochnoye
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=polunochnoye
    Processing Record 606 for ahipara
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ahipara
    Processing Record 607 for saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saskylakh
    Processing Record 608 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 609 for bethel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bethel
    Processing Record 610 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 611 for souillac
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=souillac
    Processing Record 612 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 613 for khelyulya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khelyulya
    Processing Record 614 for clyde river
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=clyde river
    Processing Record 615 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 616 for avarua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=avarua
    Processing Record 617 for ulaangom
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ulaangom
    Processing Record 618 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 619 for khandyga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khandyga
    Processing Record 620 for nyurba
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nyurba
    Processing Record 621 for laurentides
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=laurentides
    Processing Record 622 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 623 for georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=georgetown
    Processing Record 624 for oriximina
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=oriximina
    Processing Record 625 for urbano santos
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=urbano santos
    Processing Record 626 for faanui
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=faanui
    Processing Record 627 for khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khatanga
    Processing Record 628 for anito
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=anito
    Processing Record 629 for rocha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rocha
    Processing Record 630 for namibe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=namibe
    Processing Record 631 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 632 for ambilobe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ambilobe
    Processing Record 633 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 634 for geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=geraldton
    Processing Record 635 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 636 for lebu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lebu
    Processing Record 637 for kuvandyk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kuvandyk
    Processing Record 638 for broken hill
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=broken hill
    Processing Record 639 for saldanha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saldanha
    Processing Record 640 for avarua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=avarua
    Processing Record 641 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 642 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 643 for lebu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lebu
    Processing Record 644 for diego de almagro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=diego de almagro
    Processing Record 645 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 646 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 647 for san patricio
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=san patricio
    Processing Record 648 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 649 for dongying
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=dongying
    Processing Record 650 for raudeberg
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=raudeberg
    Processing Record 651 for shimoda
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=shimoda
    Processing Record 652 for san patricio
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=san patricio
    Processing Record 653 for thompson
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=thompson
    Processing Record 654 for baykalsk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=baykalsk
    Processing Record 655 for moose factory
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=moose factory
    Processing Record 656 for bethel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bethel
    Processing Record 657 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 658 for upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=upernavik
    Processing Record 659 for leningradskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=leningradskiy
    Processing Record 660 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 661 for ust-omchug
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ust-omchug
    Processing Record 662 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 663 for yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yellowknife
    Processing Record 664 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 665 for veraval
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=veraval
    Processing Record 666 for hithadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hithadhoo
    Processing Record 667 for puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto ayora
    Processing Record 668 for carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=carnarvon
    Processing Record 669 for saint-philippe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saint-philippe
    Processing Record 670 for lorengau
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lorengau
    Processing Record 671 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 672 for strenci
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=strenci
    Processing Record 673 for muncar
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=muncar
    Processing Record 674 for firminopolis
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=firminopolis
    Processing Record 675 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 676 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 677 for nome
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nome
    Processing Record 678 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 679 for cidreira
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cidreira
    Processing Record 680 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 681 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 682 for jiamusi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jiamusi
    Processing Record 683 for bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bambous virieux
    Processing Record 684 for bubaque
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bubaque
    Processing Record 685 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 686 for rawson
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rawson
    Processing Record 687 for los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=los llanos de aridane
    Processing Record 688 for pryazha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pryazha
    Processing Record 689 for rocha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rocha
    Processing Record 690 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 691 for thompson
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=thompson
    Processing Record 692 for port macquarie
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port macquarie
    Processing Record 693 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 694 for airai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=airai
    Processing Record 695 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 696 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 697 for saldanha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saldanha
    Processing Record 698 for chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=chokurdakh
    Processing Record 699 for valdivia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=valdivia
    Processing Record 700 for lauria
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lauria
    Processing Record 701 for aranda de duero
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=aranda de duero
    Processing Record 702 for moerai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=moerai
    Processing Record 703 for torres
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=torres
    Processing Record 704 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 705 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 706 for puerto colombia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto colombia
    Processing Record 707 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 708 for parabel
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=parabel
    Processing Record 709 for ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ponta do sol
    Processing Record 710 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 711 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 712 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 713 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 714 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 715 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 716 for saint george
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saint george
    Processing Record 717 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 718 for boende
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=boende
    Processing Record 719 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 720 for darnah
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=darnah
    Processing Record 721 for kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodiak
    Processing Record 722 for kavaratti
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kavaratti
    Processing Record 723 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 724 for mount gambier
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mount gambier
    Processing Record 725 for carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=carnarvon
    Processing Record 726 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 727 for arman
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arman
    Processing Record 728 for arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arraial do cabo
    Processing Record 729 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 730 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 731 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 732 for lagoa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lagoa
    Processing Record 733 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 734 for aklavik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=aklavik
    Processing Record 735 for college
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=college
    Processing Record 736 for longyearbyen
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=longyearbyen
    Processing Record 737 for labuhan
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=labuhan
    Processing Record 738 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 739 for lagoa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lagoa
    Processing Record 740 for aloleng
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=aloleng
    Processing Record 741 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 742 for chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=chokurdakh
    Processing Record 743 for leshukonskoye
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=leshukonskoye
    Processing Record 744 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 745 for hasaki
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hasaki
    Processing Record 746 for yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yellowknife
    Processing Record 747 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 748 for goderich
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=goderich
    Processing Record 749 for yar-sale
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yar-sale
    Processing Record 750 for maceio
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=maceio
    Processing Record 751 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 752 for airai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=airai
    Processing Record 753 for hithadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hithadhoo
    Processing Record 754 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 755 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 756 for tsiroanomandidy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tsiroanomandidy
    Processing Record 757 for tasiilaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tasiilaq
    Processing Record 758 for katsuura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=katsuura
    Processing Record 759 for paka
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=paka
    Processing Record 760 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 761 for mar del plata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mar del plata
    Processing Record 762 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 763 for ekibastuz
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ekibastuz
    Processing Record 764 for hirara
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hirara
    Processing Record 765 for shingu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=shingu
    Processing Record 766 for huarmey
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=huarmey
    Processing Record 767 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 768 for puerto escondido
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto escondido
    Processing Record 769 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 770 for constitucion
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=constitucion
    Processing Record 771 for bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bambous virieux
    Processing Record 772 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 773 for cap malheureux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cap malheureux
    Processing Record 774 for tawang
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tawang
    Processing Record 775 for pisco
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pisco
    Processing Record 776 for pevek
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pevek
    Processing Record 777 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 778 for zaraza
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=zaraza
    Processing Record 779 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 780 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 781 for port blair
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port blair
    Processing Record 782 for puerto escondido
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto escondido
    Processing Record 783 for ipubi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ipubi
    Processing Record 784 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 785 for bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bredasdorp
    Processing Record 786 for tadine
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tadine
    Processing Record 787 for nalut
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nalut
    Processing Record 788 for bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bathsheba
    Processing Record 789 for bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bredasdorp
    Processing Record 790 for khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khatanga
    Processing Record 791 for noshiro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=noshiro
    Processing Record 792 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 793 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 794 for ucluelet
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ucluelet
    Processing Record 795 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 796 for oneonta
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=oneonta
    Processing Record 797 for honningsvag
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=honningsvag
    Processing Record 798 for touros
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=touros
    Processing Record 799 for san quintin
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=san quintin
    Processing Record 800 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 801 for kattivakkam
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kattivakkam
    Processing Record 802 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 803 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 804 for avarua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=avarua
    Processing Record 805 for kavaratti
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kavaratti
    Processing Record 806 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 807 for kalabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kalabo
    Processing Record 808 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 809 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 810 for east london
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=east london
    Processing Record 811 for tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tuktoyaktuk
    Processing Record 812 for east london
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=east london
    Processing Record 813 for provideniya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=provideniya
    Processing Record 814 for hasaki
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hasaki
    Processing Record 815 for taltal
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=taltal
    Processing Record 816 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 817 for provideniya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=provideniya
    Processing Record 818 for umm bab
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=umm bab
    Processing Record 819 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 820 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 821 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 822 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 823 for tavda
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tavda
    Processing Record 824 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 825 for labuan
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=labuan
    Processing Record 826 for aykhal
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=aykhal
    Processing Record 827 for songkhla
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=songkhla
    Processing Record 828 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 829 for nedjo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nedjo
    Processing Record 830 for atakpame
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atakpame
    Processing Record 831 for port hardy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port hardy
    Processing Record 832 for bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bambous virieux
    Processing Record 833 for saldanha
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saldanha
    Processing Record 834 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 835 for bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bredasdorp
    Processing Record 836 for cabo san lucas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cabo san lucas
    Processing Record 837 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 838 for comodoro rivadavia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=comodoro rivadavia
    Processing Record 839 for ilulissat
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ilulissat
    Processing Record 840 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 841 for georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=georgetown
    Processing Record 842 for pisco
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pisco
    Processing Record 843 for ocampo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ocampo
    Processing Record 844 for langsa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=langsa
    Processing Record 845 for georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=georgetown
    Processing Record 846 for eirunepe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=eirunepe
    Processing Record 847 for souillac
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=souillac
    Processing Record 848 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 849 for bluefield
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluefield
    Processing Record 850 for kruisfontein
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kruisfontein
    Processing Record 851 for saint helens
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saint helens
    Processing Record 852 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 853 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 854 for sitka
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sitka
    Processing Record 855 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 856 for klaksvik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=klaksvik
    Processing Record 857 for russell
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=russell
    Processing Record 858 for soc trang
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=soc trang
    Processing Record 859 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 860 for sigli
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sigli
    Processing Record 861 for klaksvik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=klaksvik
    Processing Record 862 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 863 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 864 for goderich
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=goderich
    Processing Record 865 for najran
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=najran
    Processing Record 866 for blumberg
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=blumberg
    Processing Record 867 for bonfim
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bonfim
    Processing Record 868 for orcopampa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=orcopampa
    Processing Record 869 for pevek
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pevek
    Processing Record 870 for soyo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=soyo
    Processing Record 871 for voi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=voi
    Processing Record 872 for pangnirtung
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pangnirtung
    Processing Record 873 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 874 for torbay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=torbay
    Processing Record 875 for saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saskylakh
    Processing Record 876 for storsteinnes
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=storsteinnes
    Processing Record 877 for temir
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=temir
    Processing Record 878 for upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=upernavik
    Processing Record 879 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 880 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 881 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 882 for hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hermanus
    Processing Record 883 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 884 for lubao
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lubao
    Processing Record 885 for bluff
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bluff
    Processing Record 886 for arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arraial do cabo
    Processing Record 887 for khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=khatanga
    Processing Record 888 for nizwa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nizwa
    Processing Record 889 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 890 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 891 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 892 for yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=yellowknife
    Processing Record 893 for omsukchan
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=omsukchan
    Processing Record 894 for klaksvik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=klaksvik
    Processing Record 895 for nikolskoye
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nikolskoye
    Processing Record 896 for veraval
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=veraval
    Processing Record 897 for ampanihy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ampanihy
    Processing Record 898 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 899 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 900 for hambantota
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hambantota
    Processing Record 901 for puerto ayora
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto ayora
    Processing Record 902 for kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodiak
    Processing Record 903 for saint george
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saint george
    Processing Record 904 for nanchong
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nanchong
    Processing Record 905 for cockburn town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cockburn town
    Processing Record 906 for dawlatabad
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=dawlatabad
    Processing Record 907 for severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=severo-kurilsk
    Processing Record 908 for aksay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=aksay
    Processing Record 909 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 910 for morant bay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=morant bay
    Processing Record 911 for rio gallegos
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rio gallegos
    Processing Record 912 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 913 for chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=chokurdakh
    Processing Record 914 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 915 for richards bay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=richards bay
    Processing Record 916 for dikson
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=dikson
    Processing Record 917 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 918 for saint-philippe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=saint-philippe
    Processing Record 919 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 920 for atuona
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=atuona
    Processing Record 921 for laguna
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=laguna
    Processing Record 922 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 923 for whitianga
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=whitianga
    Processing Record 924 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 925 for kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodiak
    Processing Record 926 for malanje
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=malanje
    Processing Record 927 for belaya gora
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=belaya gora
    Processing Record 928 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 929 for thinadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=thinadhoo
    Processing Record 930 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 931 for longyearbyen
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=longyearbyen
    Processing Record 932 for paamiut
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=paamiut
    Processing Record 933 for lebu
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lebu
    Processing Record 934 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 935 for lingao
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lingao
    Processing Record 936 for east london
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=east london
    Processing Record 937 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 938 for qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=qaanaaq
    Processing Record 939 for cabo san lucas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cabo san lucas
    Processing Record 940 for qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=qaanaaq
    Processing Record 941 for griffith
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=griffith
    Processing Record 942 for thompson
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=thompson
    Processing Record 943 for barrow
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=barrow
    Processing Record 944 for ormara
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ormara
    Processing Record 945 for rabo de peixe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rabo de peixe
    Processing Record 946 for gravdal
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=gravdal
    Processing Record 947 for vao
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vao
    Processing Record 948 for airai
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=airai
    Processing Record 949 for shimoda
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=shimoda
    Processing Record 950 for ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ribeira grande
    Processing Record 951 for almeirim
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=almeirim
    Processing Record 952 for walvis bay
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=walvis bay
    Processing Record 953 for omboue
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=omboue
    Processing Record 954 for eldorado
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=eldorado
    Processing Record 955 for cayenne
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cayenne
    Processing Record 956 for verkhovazhye
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=verkhovazhye
    Processing Record 957 for ippy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ippy
    Processing Record 958 for kavieng
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kavieng
    Processing Record 959 for durham
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=durham
    Processing Record 960 for provideniya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=provideniya
    Processing Record 961 for boa vista
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=boa vista
    Processing Record 962 for alice springs
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=alice springs
    Processing Record 963 for naze
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=naze
    Processing Record 964 for upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=upernavik
    Processing Record 965 for qaqortoq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=qaqortoq
    Processing Record 966 for matara
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=matara
    Processing Record 967 for bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bredasdorp
    Processing Record 968 for bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bathsheba
    Processing Record 969 for awbari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=awbari
    Processing Record 970 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 971 for fortuna
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=fortuna
    Processing Record 972 for tasiilaq
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tasiilaq
    Processing Record 973 for sassandra
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sassandra
    Processing Record 974 for hamilton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hamilton
    Processing Record 975 for haines junction
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=haines junction
    Processing Record 976 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 977 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 978 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 979 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 980 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 981 for aykhal
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=aykhal
    Processing Record 982 for dikson
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=dikson
    Processing Record 983 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 984 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 985 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 986 for cadillac
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cadillac
    Processing Record 987 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 988 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 989 for chernaya kholunitsa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=chernaya kholunitsa
    Processing Record 990 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 991 for new norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=new norfolk
    Processing Record 992 for cape town
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cape town
    Processing Record 993 for pangnirtung
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=pangnirtung
    Processing Record 994 for bubaque
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bubaque
    Processing Record 995 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 996 for lavrentiya
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lavrentiya
    Processing Record 997 for kaitangata
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kaitangata
    Processing Record 998 for castro
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=castro
    Processing Record 999 for ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ponta do sol
    Processing Record 1000 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 1001 for esperance
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=esperance
    Processing Record 1002 for trzcianka
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=trzcianka
    Processing Record 1003 for lagoa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=lagoa
    Processing Record 1004 for simi valley
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=simi valley
    Processing Record 1005 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 1006 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 1007 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 1008 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 1009 for margate
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=margate
    Processing Record 1010 for jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jamestown
    Processing Record 1011 for beltangadi
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=beltangadi
    Processing Record 1012 for sao gabriel da cachoeira
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sao gabriel da cachoeira
    Processing Record 1013 for vaini
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vaini
    Processing Record 1014 for arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arraial do cabo
    Processing Record 1015 for eureka
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=eureka
    Processing Record 1016 for butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=butaritari
    Processing Record 1017 for kimbe
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kimbe
    Processing Record 1018 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 1019 for norman wells
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=norman wells
    Processing Record 1020 for fortuna
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=fortuna
    Processing Record 1021 for arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=arraial do cabo
    Processing Record 1022 for jardim
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=jardim
    Processing Record 1023 for ixtapa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ixtapa
    Processing Record 1024 for vestmanna
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=vestmanna
    Processing Record 1025 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 1026 for goleta
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=goleta
    Processing Record 1027 for cherskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=cherskiy
    Processing Record 1028 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 1029 for bambous virieux
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=bambous virieux
    Processing Record 1030 for hilo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hilo
    Processing Record 1031 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 1032 for te anau
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=te anau
    Processing Record 1033 for tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tuktoyaktuk
    Processing Record 1034 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 1035 for avarua
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=avarua
    Processing Record 1036 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 1037 for duluth
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=duluth
    Processing Record 1038 for ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ribeira grande
    Processing Record 1039 for hobart
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hobart
    Processing Record 1040 for kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kodiak
    Processing Record 1041 for kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kapaa
    Processing Record 1042 for ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ponta do sol
    Processing Record 1043 for grindavik
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=grindavik
    Processing Record 1044 for kahului
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=kahului
    Processing Record 1045 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 1046 for alice springs
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=alice springs
    Processing Record 1047 for punta arenas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=punta arenas
    Processing Record 1048 for faanui
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=faanui
    Processing Record 1049 for tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=tuktoyaktuk
    Processing Record 1050 for east london
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=east london
    Processing Record 1051 for zell am see
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=zell am see
    Processing Record 1052 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 1053 for ancud
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ancud
    Processing Record 1054 for ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ponta do sol
    Processing Record 1055 for nikolskoye
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=nikolskoye
    Processing Record 1056 for biltine
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=biltine
    Processing Record 1057 for ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ushuaia
    Processing Record 1058 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 1059 for beringovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=beringovskiy
    Processing Record 1060 for rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=rikitea
    Processing Record 1061 for port alfred
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=port alfred
    Processing Record 1062 for sawtell
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=sawtell
    Processing Record 1063 for busselton
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=busselton
    Processing Record 1064 for hithadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=hithadhoo
    Processing Record 1065 for dingle
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=dingle
    Processing Record 1066 for puerto cabezas
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=puerto cabezas
    Processing Record 1067 for darlowo
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=darlowo
    Processing Record 1068 for ponta do sol
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ponta do sol
    Processing Record 1069 for norden
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=norden
    Processing Record 1070 for ribeira grande
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=ribeira grande
    Processing Record 1071 for albany
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=albany
    Processing Record 1072 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 1073 for mataura
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=mataura
    Processing Record 1074 for berlevag
    http://api.openweathermap.org/data/2.5/weather?appid=3eb7f774486984bf054e7bf3d3238c00&units=imperial&q=berlevag
    -----------------------------
    Data Retrieval Complete
    -----------------------------



```python
# Store this information in a dictionary and then create a dataframe
weather_dict = { "City" : valid_cities,
                "Latitude" : valid_lat,
                "Humidity" : humidity,
                "Wind Speed" : wind_speed,
               "Temperature" : temp,
               "Cloudiness" : cloudiness}
weather_data = pd.DataFrame(weather_dict)
# confirm that our data frame has unique cities
weather_data.drop_duplicates(["City"], keep = "first")
len(weather_data.index)

```




    1074




```python
# Build a scatter plot
plt.scatter(weather_data["Latitude"], weather_data["Temperature"], marker = "o")

# Add title and label both axes
plt.title("City Latitude vs. Max Temperature (04/21/2018)")
plt.ylabel("Max Temperature (F)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("City Latitude, Max Temperature")

# Show plot
plt.show()

```


![png](output_8_0.png)



```python
# Build a scatter plot
plt.scatter(weather_data["Latitude"], weather_data["Humidity"], marker = "o")

# Add title and label both axes
plt.title("City Latitude vs. Humidity (04/21/2018)")
plt.ylabel("Humidity (%)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("City Latitude, Humidity")

# Show plot
plt.show()

```


![png](output_9_0.png)



```python
# Build a scatter plot
plt.scatter(weather_data["Latitude"], weather_data["Cloudiness"], marker = "o")

# Add title and label both axes
plt.title("City Latitude vs. Cloudiness (04/21/2018)")
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("City Latitude, Cloudiness")

# Show plot
plt.show()

```


![png](output_10_0.png)



```python
# Build a scatter plot
plt.scatter(weather_data["Latitude"], weather_data["Wind Speed"], marker = "o")

# Add title and label both axes
plt.title("City Latitude vs. Wind Speed (04/21/2018)")
plt.ylabel("Wind Speed (mph)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("City Latitude, Wind Speed")

# Show plot
plt.show()

```


![png](output_11_0.png)



```python
# Export file as a CSV
weather_data.to_csv("Output/weather.csv", index=False, header=True)
```
