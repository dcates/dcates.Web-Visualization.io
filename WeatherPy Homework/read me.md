

```python
#Observed Trends
#1: Generally speaking, cities closer to the equator are warmer
#2: Humidity increases generally as you get closer to the equator
#3: Latitudes around -50 and 60 seem to have more cities with stronger winds
```


```python
# Dependencies
import openweathermapy.core as owm
import random
import json
import requests
import pandas as pd
import matplotlib.pyplot as plt
from citipy import citipy
from config import api_key
import numpy as np
from time import gmtime, strftime
```


```python
#pulling current date and storeing in variable
nowdate = strftime("%m/%d/%Y", gmtime())
```


```python
#generating randon Latitude and Longitude
lat = np.random.uniform(-90, 90,1500)
lon = np.random.uniform(-180, 180,1500)

#putting latitude and longitude into a tuple
latlon = tuple(zip(lat, lon))

#looking up nearest cities to latitudes and longitudes generated
#putting all city lat and long into a list for city name lookup
citipycities = []
for coordinate_pair in latlon:
    lat, lon = coordinate_pair
    citipycities.append(citipy.nearest_city(lat, lon))

#looking up city names and storing in list for future use
cities = []
for city in citipycities:
    cities.append(city.city_name)

#removing duplicate city names
wodup_cities = list(set(cities))

#printing length to confirm more than 500 city names have been selected
citycount = len(wodup_cities)
print(f' The number of citys randomly selected is {citycount}')

```

     The number of citys randomly selected is 635
    


```python
# setting up url for api request
url = "http://api.openweathermap.org/data/2.5/weather?"
# setting units to pull Fahrenheit
units = "imperial"

# Building query URL
query_url = f"{url}appid={api_key}&units={units}&q="
```


```python
# set up lists to hold reponse info
#test = ["emporia", "kansas City"]
lat = []
temp = []
hum = []
cloud = []
wind = []
cntry = []
date = []
lng = []
mxtemp = []
name = []
cnt = 0
# Looping through the list of cities and perform a request for data on each city
# using a try/except as some cities do not have specific data for us to review
for city in wodup_cities:
    try:
        response = requests.get(query_url + city).json()
        lat.append(response['coord']['lat'])
        temp.append(response['main']['temp'])
        hum.append(response['main']['humidity'])
        cloud.append(response['clouds']['all'])
        wind.append(response['wind']['speed'])
        cntry.append(response['sys']['country'])
        date.append(response['dt'])
        lng.append(response['coord']['lon'])
        mxtemp.append(response['main']['temp_max'])
        name.append(response['name'])
        #print(f'Tip {'name'}: {tweet["text"]}')
        #print(f'{cnt+1}')
        print(f'Processing record {cnt+1} for the city of {name[cnt]}')
        print(f'{query_url + city}')
        #print(f"The latitude information received is: {lat}")
        #print(f"The temperature F information received is: {temp}")
        #print(f"The Humidity % information received is: {hum}")
        #print(f"The cloudiness % information received is: {cloud}")
        #print(f"The windspeed mph information received is: {wind}")
        #print(f"The country code information received is: {cntry}")
        #print(f"The date of pull information received is: {date}")
        #print(f"The longitude information received is: {lng}")
        #print(f"The max temp information received is: {mxtemp}")
        cnt = cnt + 1
    except KeyError:
        next
```

    Processing record 1 for the city of Faanui
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=faanui
    Processing record 2 for the city of Vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=vestmannaeyjar
    Processing record 3 for the city of Kamen-Rybolov
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kamen-rybolov
    Processing record 4 for the city of Bluff
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bluff
    Processing record 5 for the city of Colares
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=colares
    Processing record 6 for the city of Lima
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lima
    Processing record 7 for the city of Kuytun
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kuytun
    Processing record 8 for the city of Portland
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=portland
    Processing record 9 for the city of Neon Karlovasion
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=neon karlovasion
    Processing record 10 for the city of Pascagoula
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pascagoula
    Processing record 11 for the city of Bilibino
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bilibino
    Processing record 12 for the city of Kieta
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kieta
    Processing record 13 for the city of Karratha
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=karratha
    Processing record 14 for the city of Bireun
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bireun
    Processing record 15 for the city of Tual
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tual
    Processing record 16 for the city of Praia da Vitoria
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=praia da vitoria
    Processing record 17 for the city of Boo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=boo
    Processing record 18 for the city of Pozo Colorado
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pozo colorado
    Processing record 19 for the city of Pestretsy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pestretsy
    Processing record 20 for the city of Rivadavia
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=rivadavia
    Processing record 21 for the city of Kahului
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kahului
    Processing record 22 for the city of Carutapera
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=carutapera
    Processing record 23 for the city of Imbituba
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=imbituba
    Processing record 24 for the city of Aklavik
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=aklavik
    Processing record 25 for the city of Yarmouth
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=yarmouth
    Processing record 26 for the city of Great Yarmouth
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=great yarmouth
    Processing record 27 for the city of Pitimbu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pitimbu
    Processing record 28 for the city of Oussouye
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=oussouye
    Processing record 29 for the city of Augustdorf
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=augustdorf
    Processing record 30 for the city of Muros
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=muros
    Processing record 31 for the city of Erenhot
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=erenhot
    Processing record 32 for the city of Yanam
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=yanam
    Processing record 33 for the city of Minab
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=minab
    Processing record 34 for the city of Benjamin Hill
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=benjamin hill
    Processing record 35 for the city of Srednekolymsk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=srednekolymsk
    Processing record 36 for the city of Mackay
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mackay
    Processing record 37 for the city of Romny
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=romny
    Processing record 38 for the city of Dunmore Town
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dunmore town
    Processing record 39 for the city of Malkangiri
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=malkangiri
    Processing record 40 for the city of Saint George
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=saint george
    Processing record 41 for the city of Mar del Plata
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mar del plata
    Processing record 42 for the city of Seddon
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=seddon
    Processing record 43 for the city of Cape Town
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cape town
    Processing record 44 for the city of Bourbonnais
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bourbonnais
    Processing record 45 for the city of North Bend
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=north bend
    Processing record 46 for the city of Fiche
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=fiche
    Processing record 47 for the city of Sao Joao da Barra
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sao joao da barra
    Processing record 48 for the city of Riberalta
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=riberalta
    Processing record 49 for the city of Namatanai
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=namatanai
    Processing record 50 for the city of Autazes
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=autazes
    Processing record 51 for the city of Kawalu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kawalu
    Processing record 52 for the city of Gazanjyk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gazanjyk
    Processing record 53 for the city of Robertsport
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=robertsport
    Processing record 54 for the city of Corning
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=corning
    Processing record 55 for the city of Ibra
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ibra
    Processing record 56 for the city of Wad Rawah
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=wad rawah
    Processing record 57 for the city of San Cristobal
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=san cristobal
    Processing record 58 for the city of Avera
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=avera
    Processing record 59 for the city of Butembo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=butembo
    Processing record 60 for the city of Lixourion
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lixourion
    Processing record 61 for the city of Budesti
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=budesti
    Processing record 62 for the city of Verkhniy Avzyan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=verkhniy avzyan
    Processing record 63 for the city of Alice Springs
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=alice springs
    Processing record 64 for the city of Taiyuan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=taiyuan
    Processing record 65 for the city of Esperance
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=esperance
    Processing record 66 for the city of Delhi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=delhi
    Processing record 67 for the city of Yavaros
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=yavaros
    Processing record 68 for the city of Nuuk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nuuk
    Processing record 69 for the city of Takoradi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=takoradi
    Processing record 70 for the city of Neiafu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=neiafu
    Processing record 71 for the city of Muscat
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=muscat
    Processing record 72 for the city of Grimmen
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=grimmen
    Processing record 73 for the city of Lata
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lata
    Processing record 74 for the city of Mataura
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mataura
    Processing record 75 for the city of Wheeling
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=wheeling
    Processing record 76 for the city of Margate
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=margate
    Processing record 77 for the city of Ponta Delgada
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ponta delgada
    Processing record 78 for the city of Buraydah
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=buraydah
    Processing record 79 for the city of Lumeje
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lumeje
    Processing record 80 for the city of Ramona
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ramona
    Processing record 81 for the city of Nanortalik
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nanortalik
    Processing record 82 for the city of Sao Filipe
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sao filipe
    Processing record 83 for the city of Busselton
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=busselton
    Processing record 84 for the city of Monselice
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=monselice
    Processing record 85 for the city of Mount Isa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mount isa
    Processing record 86 for the city of Valdez
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=valdez
    Processing record 87 for the city of Santa Fe
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=santa fe
    Processing record 88 for the city of Gotsu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gotsu
    Processing record 89 for the city of Nikolskoye
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nikolskoye
    Processing record 90 for the city of Koumac
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=koumac
    Processing record 91 for the city of Fernley
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=fernley
    Processing record 92 for the city of Shimoda
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=shimoda
    Processing record 93 for the city of Yeppoon
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=yeppoon
    Processing record 94 for the city of Tazovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tazovskiy
    Processing record 95 for the city of Frankfort
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=frankfort
    Processing record 96 for the city of Port Alfred
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=port alfred
    Processing record 97 for the city of Arraial do Cabo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=arraial do cabo
    Processing record 98 for the city of Jacareacanga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jacareacanga
    Processing record 99 for the city of San Carlos de Bariloche
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=san carlos de bariloche
    Processing record 100 for the city of Novita
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=novita
    Processing record 101 for the city of Bonfim
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bonfim
    Processing record 102 for the city of Kruisfontein
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kruisfontein
    Processing record 103 for the city of Pyapon
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pyapon
    Processing record 104 for the city of Bathsheba
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bathsheba
    Processing record 105 for the city of Dalvik
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dalvik
    Processing record 106 for the city of Jerecuaro
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jerecuaro
    Processing record 107 for the city of Kasongo-Lunda
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kasongo-lunda
    Processing record 108 for the city of Creel
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=creel
    Processing record 109 for the city of Saint-Philippe
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=saint-philippe
    Processing record 110 for the city of Kangaatsiaq
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kangaatsiaq
    Processing record 111 for the city of Rio Gallegos
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=rio gallegos
    Processing record 112 for the city of Shyryayeve
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=shyryayeve
    Processing record 113 for the city of Bensonville
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bensonville
    Processing record 114 for the city of Iqaluit
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=iqaluit
    Processing record 115 for the city of Barrow
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=barrow
    Processing record 116 for the city of Bandarbeyla
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bandarbeyla
    Processing record 117 for the city of Missoula
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=missoula
    Processing record 118 for the city of Cleveland
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cleveland
    Processing record 119 for the city of Avallon
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=avallon
    Processing record 120 for the city of Loiza
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=loiza
    Processing record 121 for the city of Amapa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=amapa
    Processing record 122 for the city of Gravdal
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gravdal
    Processing record 123 for the city of Glenwood Springs
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=glenwood springs
    Processing record 124 for the city of Rudnogorsk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=rudnogorsk
    Processing record 125 for the city of Hilo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hilo
    Processing record 126 for the city of Kauswagan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kauswagan
    Processing record 127 for the city of Kautokeino
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kautokeino
    Processing record 128 for the city of Berlevag
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=berlevag
    Processing record 129 for the city of Naze
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=naze
    Processing record 130 for the city of Avarua
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=avarua
    Processing record 131 for the city of Khatanga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=khatanga
    Processing record 132 for the city of Posse
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=posse
    Processing record 133 for the city of Havre-Saint-Pierre
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=havre-saint-pierre
    Processing record 134 for the city of Gairo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gairo
    Processing record 135 for the city of Santa Barbara
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=santa barbara
    Processing record 136 for the city of Onega
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=onega
    Processing record 137 for the city of Coquimbo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=coquimbo
    Processing record 138 for the city of Havelock
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=havelock
    Processing record 139 for the city of Ilulissat
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ilulissat
    Processing record 140 for the city of Jerez
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jerez
    Processing record 141 for the city of Tecoanapa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tecoanapa
    Processing record 142 for the city of Victoria
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=victoria
    Processing record 143 for the city of Rurrenabaque
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=rurrenabaque
    Processing record 144 for the city of Kaitangata
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kaitangata
    Processing record 145 for the city of Ometepec
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ometepec
    Processing record 146 for the city of Isangel
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=isangel
    Processing record 147 for the city of Codrington
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=codrington
    Processing record 148 for the city of Voh
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=voh
    Processing record 149 for the city of Juba
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=juba
    Processing record 150 for the city of Yar-Sale
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=yar-sale
    Processing record 151 for the city of Araguari
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=araguari
    Processing record 152 for the city of Chokurdakh
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=chokurdakh
    Processing record 153 for the city of Nampula
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nampula
    Processing record 154 for the city of Santiago
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=santiago
    Processing record 155 for the city of Pevek
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pevek
    Processing record 156 for the city of Bojnurd
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bojnurd
    Processing record 157 for the city of Inirida
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=inirida
    Processing record 158 for the city of Acapulco
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=acapulco
    Processing record 159 for the city of Cordoba
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cordoba
    Processing record 160 for the city of Senanga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=senanga
    Processing record 161 for the city of Preobrazheniye
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=preobrazheniye
    Processing record 162 for the city of Kazachinskoye
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kazachinskoye
    Processing record 163 for the city of Syracuse
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=syracuse
    Processing record 164 for the city of Marawi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=marawi
    Processing record 165 for the city of Mislinja
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mislinja
    Processing record 166 for the city of Geraldton
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=geraldton
    Processing record 167 for the city of Gbadolite
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gbadolite
    Processing record 168 for the city of Morant Bay
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=morant bay
    Processing record 169 for the city of Primorsko-Akhtarsk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=primorsko-akhtarsk
    Processing record 170 for the city of Lusambo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lusambo
    Processing record 171 for the city of Tautira
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tautira
    Processing record 172 for the city of Vila Velha
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=vila velha
    Processing record 173 for the city of Harper
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=harper
    Processing record 174 for the city of Te Anau
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=te anau
    Processing record 175 for the city of Grand Gaube
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=grand gaube
    Processing record 176 for the city of Diffa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=diffa
    Processing record 177 for the city of Okha
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=okha
    Processing record 178 for the city of Moerai
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=moerai
    Processing record 179 for the city of Taoudenni
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=taoudenni
    Processing record 180 for the city of Tongliao
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tongliao
    Processing record 181 for the city of High Level
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=high level
    Processing record 182 for the city of Pisco
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pisco
    Processing record 183 for the city of Sindor
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sindor
    Processing record 184 for the city of Keti Bandar
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=keti bandar
    Processing record 185 for the city of Roald
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=roald
    Processing record 186 for the city of Clarence Town
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=clarence town
    Processing record 187 for the city of Shishou
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=shishou
    Processing record 188 for the city of Hluti
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hluti
    Processing record 189 for the city of Joetsu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=joetsu
    Processing record 190 for the city of Kochubey
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kochubey
    Processing record 191 for the city of Victoria
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=labuan
    Processing record 192 for the city of Tuatapere
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tuatapere
    Processing record 193 for the city of Whitehorse
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=whitehorse
    Processing record 194 for the city of Chuy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=chuy
    Processing record 195 for the city of Izhma
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=izhma
    Processing record 196 for the city of Bismarck
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bismarck
    Processing record 197 for the city of Agadir
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=agadir
    Processing record 198 for the city of Shinyanga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=shinyanga
    Processing record 199 for the city of Manohar Thana
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=manohar thana
    Processing record 200 for the city of Thompson
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=thompson
    Processing record 201 for the city of Anloga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=anloga
    Processing record 202 for the city of Toamasina
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=toamasina
    Processing record 203 for the city of Casma
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=casma
    Processing record 204 for the city of Touros
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=touros
    Processing record 205 for the city of Coihaique
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=coihaique
    Processing record 206 for the city of Lagos
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lagos
    Processing record 207 for the city of Bambanglipuro
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bambanglipuro
    Processing record 208 for the city of Ushuaia
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ushuaia
    Processing record 209 for the city of Bolshaya Glushitsa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bolshaya glushitsa
    Processing record 210 for the city of Caravelas
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=caravelas
    Processing record 211 for the city of Matane
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=matane
    Processing record 212 for the city of Adrar
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=adrar
    Processing record 213 for the city of Khandyga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=khandyga
    Processing record 214 for the city of Luderitz
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=luderitz
    Processing record 215 for the city of Horconcitos
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=horconcitos
    Processing record 216 for the city of Bow Island
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bow island
    Processing record 217 for the city of Awbari
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=awbari
    Processing record 218 for the city of Turayf
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=turayf
    Processing record 219 for the city of Puerto Escondido
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=puerto escondido
    Processing record 220 for the city of Grand-Santi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=grand-santi
    Processing record 221 for the city of Tezu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tezu
    Processing record 222 for the city of Saint-Augustin
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=saint-augustin
    Processing record 223 for the city of Souillac
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=souillac
    Processing record 224 for the city of Ixtapa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ixtapa
    Processing record 225 for the city of Freeport
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=freeport
    Processing record 226 for the city of Hithadhoo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hithadhoo
    Processing record 227 for the city of Lososina
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lososina
    Processing record 228 for the city of Ekhabi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ekhabi
    Processing record 229 for the city of Mogadishu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mogadishu
    Processing record 230 for the city of Las Cruces
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=las cruces
    Processing record 231 for the city of Santa Isabel do Rio Negro
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=santa isabel do rio negro
    Processing record 232 for the city of Lorengau
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lorengau
    Processing record 233 for the city of Mahebourg
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mahebourg
    Processing record 234 for the city of Torbay
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=torbay
    Processing record 235 for the city of Hirara
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hirara
    Processing record 236 for the city of Oranjemund
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=oranjemund
    Processing record 237 for the city of Ponta do Sol
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ponta do sol
    Processing record 238 for the city of Albany
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=albany
    Processing record 239 for the city of Kavaratti
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kavaratti
    Processing record 240 for the city of Nueve de Julio
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nueve de julio
    Processing record 241 for the city of Tokur
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tokur
    Processing record 242 for the city of Castro
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=castro
    Processing record 243 for the city of Constitucion
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=constitucion
    Processing record 244 for the city of Dwarka
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dwarka
    Processing record 245 for the city of Cherskiy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cherskiy
    Processing record 246 for the city of Kaeo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kaeo
    Processing record 247 for the city of Bereda
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bereda
    Processing record 248 for the city of Dzhebariki-Khaya
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dzhebariki-khaya
    Processing record 249 for the city of Katsuura
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=katsuura
    Processing record 250 for the city of Choix
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=choix
    Processing record 251 for the city of New Norfolk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=new norfolk
    Processing record 252 for the city of Walvis Bay
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=walvis bay
    Processing record 253 for the city of Ust-Ilimsk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ust-ilimsk
    Processing record 254 for the city of Jalu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jalu
    Processing record 255 for the city of Smithers
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=smithers
    Processing record 256 for the city of Lere
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lere
    Processing record 257 for the city of Brenes
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=brenes
    Processing record 258 for the city of Miri
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=miri
    Processing record 259 for the city of Gat
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gat
    Processing record 260 for the city of Dum Duma
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dum duma
    Processing record 261 for the city of Gombong
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gombong
    Processing record 262 for the city of Huarmey
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=huarmey
    Processing record 263 for the city of Vrangel
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=vrangel
    Processing record 264 for the city of Broken Hill
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=broken hill
    Processing record 265 for the city of Clyde River
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=clyde river
    Processing record 266 for the city of Troy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=troy
    Processing record 267 for the city of Hambantota
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hambantota
    Processing record 268 for the city of San Jose del Guaviare
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=san jose del guaviare
    Processing record 269 for the city of Lianzhou
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lianzhou
    Processing record 270 for the city of Tura
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tura
    Processing record 271 for the city of Port Macquarie
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=port macquarie
    Processing record 272 for the city of Maun
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=maun
    Processing record 273 for the city of Nador
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nador
    Processing record 274 for the city of Suicheng
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=suicheng
    Processing record 275 for the city of Port Lincoln
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=port lincoln
    Processing record 276 for the city of Hope
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hope
    Processing record 277 for the city of Atuona
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=atuona
    Processing record 278 for the city of Anadyr
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=anadyr
    Processing record 279 for the city of Cururupu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cururupu
    Processing record 280 for the city of Puerto Ayora
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=puerto ayora
    Processing record 281 for the city of Bull Savanna
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bull savanna
    Processing record 282 for the city of Beloha
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=beloha
    Processing record 283 for the city of College
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=college
    Processing record 284 for the city of Charlestown
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=charlestown
    Processing record 285 for the city of Gasa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gasa
    Processing record 286 for the city of Oranjestad
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=oranjestad
    Processing record 287 for the city of Albanel
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=albanel
    Processing record 288 for the city of Genhe
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=genhe
    Processing record 289 for the city of Jodhpur
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jodhpur
    Processing record 290 for the city of Behbahan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=behbahan
    Processing record 291 for the city of Kinablangan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kinablangan
    Processing record 292 for the city of Dosso
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dosso
    Processing record 293 for the city of Chernaya Kholunitsa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=chernaya kholunitsa
    Processing record 294 for the city of Guamuchil
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=guamuchil
    Processing record 295 for the city of Santa Cruz de Tenerife
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=santa cruz de tenerife
    Processing record 296 for the city of Strelka
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=strelka
    Processing record 297 for the city of Nome
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nome
    Processing record 298 for the city of Aldergrove
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=aldergrove
    Processing record 299 for the city of East London
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=east london
    Processing record 300 for the city of Atar
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=atar
    Processing record 301 for the city of Las Palmas
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=las palmas
    Processing record 302 for the city of Hasaki
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hasaki
    Processing record 303 for the city of Ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ostrovnoy
    Processing record 304 for the city of Rio Grande
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=rio grande
    Processing record 305 for the city of Zeya
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=zeya
    Processing record 306 for the city of Erzin
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=erzin
    Processing record 307 for the city of Guerrero Negro
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=guerrero negro
    Processing record 308 for the city of Khasan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=khasan
    Processing record 309 for the city of Hobyo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hobyo
    Processing record 310 for the city of Cap Malheureux
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cap malheureux
    Processing record 311 for the city of Amga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=amga
    Processing record 312 for the city of Carnarvon
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=carnarvon
    Processing record 313 for the city of Boden
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=boden
    Processing record 314 for the city of Kulhudhuffushi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kulhudhuffushi
    Processing record 315 for the city of Shakawe
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=shakawe
    Processing record 316 for the city of Georgetown
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=georgetown
    Processing record 317 for the city of Jining
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jining
    Processing record 318 for the city of Meadow Lake
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=meadow lake
    Processing record 319 for the city of Kirkland Lake
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kirkland lake
    Processing record 320 for the city of Gondanglegi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gondanglegi
    Processing record 321 for the city of Tadine
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tadine
    Processing record 322 for the city of Yulara
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=yulara
    Processing record 323 for the city of Sanbu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sanbu
    Processing record 324 for the city of Cayenne
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cayenne
    Processing record 325 for the city of Vostok
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=vostok
    Processing record 326 for the city of Mabaruma
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mabaruma
    Processing record 327 for the city of Ostersund
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ostersund
    Processing record 328 for the city of Bethel
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bethel
    Processing record 329 for the city of Hobart
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hobart
    Processing record 330 for the city of Macultepec
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=macultepec
    Processing record 331 for the city of Los Llanos de Aridane
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=los llanos de aridane
    Processing record 332 for the city of Mehamn
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mehamn
    Processing record 333 for the city of Garissa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=garissa
    Processing record 334 for the city of Ouro Fino
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ouro fino
    Processing record 335 for the city of Vaitape
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=vaitape
    Processing record 336 for the city of Longyearbyen
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=longyearbyen
    Processing record 337 for the city of Lavrentiya
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lavrentiya
    Processing record 338 for the city of San Pedro
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=san pedro
    Processing record 339 for the city of Ribeira Grande
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ribeira grande
    Processing record 340 for the city of Honiara
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=honiara
    Processing record 341 for the city of Butaritari
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=butaritari
    Processing record 342 for the city of Upernavik
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=upernavik
    Processing record 343 for the city of Dunedin
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dunedin
    Processing record 344 for the city of Henties Bay
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=henties bay
    Processing record 345 for the city of Airai
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=airai
    Processing record 346 for the city of Comodoro Rivadavia
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=comodoro rivadavia
    Processing record 347 for the city of Lerwick
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lerwick
    Processing record 348 for the city of Araouane
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=araouane
    Processing record 349 for the city of Bredasdorp
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bredasdorp
    Processing record 350 for the city of Kostroma
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kostroma
    Processing record 351 for the city of Hermanus
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hermanus
    Processing record 352 for the city of Iquitos
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=iquitos
    Processing record 353 for the city of Duldurga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=duldurga
    Processing record 354 for the city of Fort Walton Beach
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=fort walton beach
    Processing record 355 for the city of Shaoyang
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=shaoyang
    Processing record 356 for the city of Ilhabela
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ilhabela
    Processing record 357 for the city of Barcelos
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=barcelos
    Processing record 358 for the city of Lagoa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lagoa
    Processing record 359 for the city of Bowling Green
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bowling green
    Processing record 360 for the city of Mangrol
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mangrol
    Processing record 361 for the city of Kargopol
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kargopol
    Processing record 362 for the city of Tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tuktoyaktuk
    Processing record 363 for the city of Azangaro
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=azangaro
    Processing record 364 for the city of Chicama
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=chicama
    Processing record 365 for the city of Vaini
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=vaini
    Processing record 366 for the city of Dikson
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dikson
    Processing record 367 for the city of Itaituba
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=itaituba
    Processing record 368 for the city of Buala
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=buala
    Processing record 369 for the city of Sestri Levante
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sestri levante
    Processing record 370 for the city of Jamestown
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jamestown
    Processing record 371 for the city of Noumea
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=noumea
    Processing record 372 for the city of Kokopo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kokopo
    Processing record 373 for the city of Alofi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=alofi
    Processing record 374 for the city of Paraiso
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=paraiso
    Processing record 375 for the city of Ramenskoye
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ramenskoye
    Processing record 376 for the city of Coracora
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=coracora
    Processing record 377 for the city of Lubango
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lubango
    Processing record 378 for the city of Kempten
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kempten
    Processing record 379 for the city of Beruwala
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=beruwala
    Processing record 380 for the city of Ukiah
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ukiah
    Processing record 381 for the city of Port Moresby
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=port moresby
    Processing record 382 for the city of Itarema
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=itarema
    Processing record 383 for the city of Huizhou
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=huizhou
    Processing record 384 for the city of Awjilah
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=awjilah
    Processing record 385 for the city of Chipinge
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=chipinge
    Processing record 386 for the city of Sikeston
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sikeston
    Processing record 387 for the city of Skjervoy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=skjervoy
    Processing record 388 for the city of Road Town
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=road town
    Processing record 389 for the city of Aykhal
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=aykhal
    Processing record 390 for the city of Poronaysk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=poronaysk
    Processing record 391 for the city of Qaanaaq
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=qaanaaq
    Processing record 392 for the city of Lasa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lasa
    Processing record 393 for the city of Landerneau
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=landerneau
    Processing record 394 for the city of Belyy Yar
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=belyy yar
    Processing record 395 for the city of Saint-Joseph
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=saint-joseph
    Processing record 396 for the city of Mount Gambier
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mount gambier
    Processing record 397 for the city of Zhigansk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=zhigansk
    Processing record 398 for the city of Socorro
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=socorro
    Processing record 399 for the city of Omsukchan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=omsukchan
    Processing record 400 for the city of Hornepayne
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hornepayne
    Processing record 401 for the city of Sitka
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sitka
    Processing record 402 for the city of Amazar
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=amazar
    Processing record 403 for the city of Saint-Pierre
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=saint-pierre
    Processing record 404 for the city of Marsa Matruh
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=marsa matruh
    Processing record 405 for the city of Kurilsk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kurilsk
    Processing record 406 for the city of Fowa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=fowa
    Processing record 407 for the city of Baherden
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=baherden
    Processing record 408 for the city of Taitung
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=taitung
    Processing record 409 for the city of Gornyak
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gornyak
    Processing record 410 for the city of Khani
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=khani
    Processing record 411 for the city of Halifax
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=halifax
    Processing record 412 for the city of Roebourne
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=roebourne
    Processing record 413 for the city of Arrifes
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=arrifes
    Processing record 414 for the city of Sibolga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sibolga
    Processing record 415 for the city of Port Elizabeth
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=port elizabeth
    Processing record 416 for the city of Severo-Kurilsk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=severo-kurilsk
    Processing record 417 for the city of Kiruna
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kiruna
    Processing record 418 for the city of Maniitsoq
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=maniitsoq
    Processing record 419 for the city of Acari
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=acari
    Processing record 420 for the city of Provideniya
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=provideniya
    Processing record 421 for the city of San Juan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=san juan
    Processing record 422 for the city of Natchitoches
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=natchitoches
    Processing record 423 for the city of Komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=komsomolskiy
    Processing record 424 for the city of Lang Suan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lang suan
    Processing record 425 for the city of Omboue
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=omboue
    Processing record 426 for the city of Poya
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=poya
    Processing record 427 for the city of Saint-Georges
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=saint-georges
    Processing record 428 for the city of Severo-Yeniseyskiy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=severo-yeniseyskiy
    Processing record 429 for the city of Kavieng
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kavieng
    Processing record 430 for the city of San Diego
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=san diego
    Processing record 431 for the city of Kaniama
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kaniama
    Processing record 432 for the city of Beringovskiy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=beringovskiy
    Processing record 433 for the city of Kaduqli
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kaduqli
    Processing record 434 for the city of Tigil
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tigil
    Processing record 435 for the city of Ushtobe
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ushtobe
    Processing record 436 for the city of Dorchester
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dorchester
    Processing record 437 for the city of Bambous Virieux
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bambous virieux
    Processing record 438 for the city of Valls
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=valls
    Processing record 439 for the city of Lakatoro
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lakatoro
    Processing record 440 for the city of Port-Gentil
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=port-gentil
    Processing record 441 for the city of Verkh-Usugli
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=verkh-usugli
    Processing record 442 for the city of Tasiilaq
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tasiilaq
    Processing record 443 for the city of Rikitea
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=rikitea
    Processing record 444 for the city of Sibay
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sibay
    Processing record 445 for the city of Tilichiki
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tilichiki
    Processing record 446 for the city of Chilliwack
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=chilliwack
    Processing record 447 for the city of Orchard Homes
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=orchard homes
    Processing record 448 for the city of Pratapgarh
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pratapgarh
    Processing record 449 for the city of Egvekinot
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=egvekinot
    Processing record 450 for the city of Hastings
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hastings
    Processing record 451 for the city of Gambela
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gambela
    Processing record 452 for the city of Cherdyn
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cherdyn
    Processing record 453 for the city of Ancud
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ancud
    Processing record 454 for the city of San Jose de Rio Tinto
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=san jose de rio tinto
    Processing record 455 for the city of Xichang
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=xichang
    Processing record 456 for the city of Goderich
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=goderich
    Processing record 457 for the city of Campina Verde
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=campina verde
    Processing record 458 for the city of Iskateley
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=iskateley
    Processing record 459 for the city of Vila Franca do Campo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=vila franca do campo
    Processing record 460 for the city of Namibe
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=namibe
    Processing record 461 for the city of Bangassou
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bangassou
    Processing record 462 for the city of Zemio
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=zemio
    Processing record 463 for the city of Bulgan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bulgan
    Processing record 464 for the city of Flinders
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=flinders
    Processing record 465 for the city of Port-Cartier
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=port-cartier
    Processing record 466 for the city of Boyuibe
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=boyuibe
    Processing record 467 for the city of Kodinsk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kodinsk
    Processing record 468 for the city of Cidreira
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cidreira
    Processing record 469 for the city of Tiksi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tiksi
    Processing record 470 for the city of Aripuana
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=aripuana
    Processing record 471 for the city of Gwadar
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=gwadar
    Processing record 472 for the city of Bela
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bela
    Processing record 473 for the city of Nuristan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nuristan
    Processing record 474 for the city of Dezhou
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=dezhou
    Processing record 475 for the city of San Patricio
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=san patricio
    Processing record 476 for the city of La Ronge
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=la ronge
    Processing record 477 for the city of Vardo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=vardo
    Processing record 478 for the city of Punta Arenas
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=punta arenas
    Processing record 479 for the city of Nepomuceno
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nepomuceno
    Processing record 480 for the city of Talin
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=talin
    Processing record 481 for the city of Boshan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=boshan
    Processing record 482 for the city of Labuhan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=labuhan
    Processing record 483 for the city of Yerbogachen
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=yerbogachen
    Processing record 484 for the city of Saldanha
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=saldanha
    Processing record 485 for the city of Sioux Lookout
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sioux lookout
    Processing record 486 for the city of Pacific Grove
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pacific grove
    Processing record 487 for the city of Penzance
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=penzance
    Processing record 488 for the city of Edd
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=edd
    Processing record 489 for the city of Pulawy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pulawy
    Processing record 490 for the city of Ambon
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ambon
    Processing record 491 for the city of Port Said
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=port said
    Processing record 492 for the city of Mayahi
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mayahi
    Processing record 493 for the city of Birjand
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=birjand
    Processing record 494 for the city of Ahipara
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ahipara
    Processing record 495 for the city of Sorland
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sorland
    Processing record 496 for the city of Sao Miguel do Araguaia
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sao miguel do araguaia
    Processing record 497 for the city of Arlit
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=arlit
    Processing record 498 for the city of Fairbanks
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=fairbanks
    Processing record 499 for the city of Zhaotong
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=zhaotong
    Processing record 500 for the city of Nanzhou
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=nanzhou
    Processing record 501 for the city of Ketchikan
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ketchikan
    Processing record 502 for the city of Husainabad
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=husainabad
    Processing record 503 for the city of Angoche
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=angoche
    Processing record 504 for the city of Kununurra
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kununurra
    Processing record 505 for the city of Sharjah
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=sharjah
    Processing record 506 for the city of Lebu
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=lebu
    Processing record 507 for the city of Aiquile
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=aiquile
    Processing record 508 for the city of Salalah
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=salalah
    Processing record 509 for the city of Cervo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cervo
    Processing record 510 for the city of Cabo San Lucas
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cabo san lucas
    Processing record 511 for the city of Illela
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=illela
    Processing record 512 for the city of Yellowknife
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=yellowknife
    Processing record 513 for the city of Turukhansk
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=turukhansk
    Processing record 514 for the city of Aranos
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=aranos
    Processing record 515 for the city of Mbuyapey
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mbuyapey
    Processing record 516 for the city of Ust-Nera
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ust-nera
    Processing record 517 for the city of Pop
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pop
    Processing record 518 for the city of Wagga Wagga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=wagga wagga
    Processing record 519 for the city of Mwinilunga
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=mwinilunga
    Processing record 520 for the city of Tanout
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tanout
    Processing record 521 for the city of Half Moon Bay
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=half moon bay
    Processing record 522 for the city of Parkes
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=parkes
    Processing record 523 for the city of Byron Bay
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=byron bay
    Processing record 524 for the city of Valparaiso
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=valparaiso
    Processing record 525 for the city of Brokopondo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=brokopondo
    Processing record 526 for the city of Jati
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jati
    Processing record 527 for the city of Buin
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=buin
    Processing record 528 for the city of Norman Wells
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=norman wells
    Processing record 529 for the city of Calbuco
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=calbuco
    Processing record 530 for the city of Saskylakh
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=saskylakh
    Processing record 531 for the city of Yuzhnyy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=yuzhnyy
    Processing record 532 for the city of Ulaanbaatar
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ulaanbaatar
    Processing record 533 for the city of Hamilton
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=hamilton
    Processing record 534 for the city of Kelso
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kelso
    Processing record 535 for the city of Jinchang
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jinchang
    Processing record 536 for the city of Beitbridge
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=beitbridge
    Processing record 537 for the city of Taltal
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=taltal
    Processing record 538 for the city of Itacoatiara
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=itacoatiara
    Processing record 539 for the city of Kapaa
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kapaa
    Processing record 540 for the city of Bumba
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=bumba
    Processing record 541 for the city of Alice
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=alice
    Processing record 542 for the city of Kalmunai
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kalmunai
    Processing record 543 for the city of Manaus
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=manaus
    Processing record 544 for the city of Pangnirtung
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=pangnirtung
    Processing record 545 for the city of Vanimo
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=vanimo
    Processing record 546 for the city of Tommot
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=tommot
    Processing record 547 for the city of Santo Amaro da Imperatriz
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=santo amaro da imperatriz
    Processing record 548 for the city of Cedar City
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=cedar city
    Processing record 549 for the city of Port Blair
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=port blair
    Processing record 550 for the city of Muli
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=muli
    Processing record 551 for the city of Esmeraldas
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=esmeraldas
    Processing record 552 for the city of Natal
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=natal
    Processing record 553 for the city of Kodiak
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=kodiak
    Processing record 554 for the city of Digha
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=digha
    Processing record 555 for the city of Ondjiva
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=ondjiva
    Processing record 556 for the city of Leningradskiy
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=leningradskiy
    Processing record 557 for the city of Manokwari
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=manokwari
    Processing record 558 for the city of Conselheiro Lafaiete
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=conselheiro lafaiete
    Processing record 559 for the city of Jiangyou
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=jiangyou
    Processing record 560 for the city of Biasca
    http://api.openweathermap.org/data/2.5/weather?appid=9c0b81722091dfebaf6da86ea9248bf1&units=imperial&q=biasca
    


```python
# creating a dataframe
weather_dict = {
    "City": name,
    "Lat": lat,
    "Temp": temp,
    "Humidity": hum,
    "Cloudiness" : cloud,
    "Wind Speed" : wind,
    "Country" : cntry,
    "Date" : date,
    "Lng" : lng,
    "Max Temp" : mxtemp
}
weather_data = pd.DataFrame(weather_dict)
#saving the dataframe to csv
weather_data.to_csv("output/Weather Data Frame.csv")
```


```python
#CITY LATITUDE V MAX TEMP
# Building the scatter plot
plt.scatter(weather_data["Lat"], weather_data["Temp"], marker="o")

# adding labels
plt.title(f'City Latitude vs. Max Tempurature {nowdate}')
#(f'Tip {counter}: {tweet["text"]}')
plt.ylabel("Max Temperature (F)")
plt.xlabel("Latitude")
plt.grid(True)

# Saving the figure
plt.savefig("output/City Latitude vs. Max Tempurature.png")

# Showing plot
plt.show()
```


![png](output_7_0.png)



```python
#CITY LATITUDE V HUMIDITY
# Building the scatter plot
plt.scatter(weather_data["Lat"], weather_data["Humidity"], marker="o")

# adding labels
plt.title(f'City Latitude Vs. Humidity {nowdate}')
plt.ylabel("Humidity (%)")
plt.xlabel("Latitude")
plt.grid(True)

# Saving the figure
# Saving the figure
plt.savefig("output/City Latitude Vs. Humidity.png")

# Show plot
plt.show()
```


![png](output_8_0.png)



```python
#CITY LATITUDE V CLOUDINESS
# Building the scatter plot
plt.scatter(weather_data["Lat"], weather_data["Cloudiness"], marker="o")

# adding labels
plt.title(f'City Latitude vs. Cloudiness {nowdate}')
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")
plt.grid(True)

# Saving the figure
plt.savefig("output/City Latitude vs. Cloudiness.png")

# Showing plot
plt.show()
```


![png](output_9_0.png)



```python
#CITY LATITUDE V WINDSPEED
# Building the scatter plot
plt.scatter(weather_data["Lat"], weather_data["Wind Speed"], marker="o")

# adding labels
plt.title(f'City Latitude vs. Wind Speed {nowdate}')
plt.ylabel("Wind Speed (mph)")
plt.xlabel("Latitude")
plt.grid(True)

# Saving the figure
plt.savefig("output/City Latitude vs. Wind Speed.png")

# Showing plot
plt.show()
```


![png](output_10_0.png)

