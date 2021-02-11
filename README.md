This is a homework Assignment from SMU Bootcamp:

WeatheryPy

VacationPY 

weatherpy:

The Python code randomly selects a group of 500+ cities across the world. Then, the code collects data from the OpenWeatherMap API to create a representatitve model of weather across world cities. The API data is used to graph the following relationships:
Temperature (F) vs. Latitude
Humidity (%) vs. Latitude
Cloudiness (%) vs. Latitude
Wind Speed (mph) vs. Latitude


Due to the live weather data being used running will generate different city data.  City data is generally given between 500 and 700 random cities.  Having access to both an api for the weather and a google api key is necessary


sample code : 

lat_lngs = []
cities = []

# Create a set of random lat and lng combinations
lats = np.random.uniform(lat_range[0], lat_range[1], size=1500)
lngs = np.random.uniform(lng_range[0], lng_range[1], size=1500)
lat_lngs = zip(lats, lngs)

# Identify nearest city for each lat, lng combination
for lat_lng in lat_lngs:
    city = citipy.nearest_city(lat_lng[0], lat_lng[1]).city_name
    
    # If the city is unique, then add it to a our cities list
    if city not in cities:
        cities.append(city)

# Print the city count to confirm sufficient count
len(cities)


 vacationpy:
 google api key is required.  due to the heatmaping extensions will be needed for gmaps and and extension for the overlay to display correctly 

 pulls weather data to find randomly find the best vacation/retimrement spots 


example code:

# NOTE: Do not change any of the code in this cell

# Using the template add the hotel marks to the heatmap
hotels = []

# Loop through narrowed down dataframe to get nearest hotel
for city in range(len(indexed_hotspot_retire["City"])):

    lat = indexed_hotspot_retire.loc[city]["Latitude"]
    lng = indexed_hotspot_retire.loc[city]["Longitude"]

    city_coords = f"{lat},{lng}"

    params = {
        "location": city_coords, 
        "types": "lodging",
        "radius": 5000,
        "key": g_key
    }

    base_url = "https://maps.googleapis.com/maps/api/place/nearbysearch/json"   

    hotel_request = requests.get(base_url, params=params)
    hotel_response = hotel_request.json()

    try:
        hotels.append(hotel_response["results"][0]["name"])
    except:
        hotels.append("Nearest hotel not found")

# Dataframe with nearest hotel
indexed_hotspot_retire["Nearest Hotel"] = hotels
indexed_hotspot_retire


The limitations of both project data sets are they are random generated and each run without saving to a csv or variable will cause changed data.   Also api may require some monitary compensation after a number of use. 



reference: 

 https://developers.google.com/maps/reporting/gmp-reporting 

 http://api.openweathermap.org/data/2.5/weather

 