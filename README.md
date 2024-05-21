# nosql-challenge

recieved help from chatGPT to make the following: 

# Change the data type from String to Decimal for longitude and latitude

establishments.update_many(
    {},
    [
        {
            "$set": {
                "geocode.longitude": {"$convert": {"input": "$geocode.longitude", "to": "double", "onError": None, "onNull": None}},
                "geocode.latitude": {"$convert": {"input": "$geocode.latitude", "to": "double", "onError": None, "onNull": None}}
            }
        }
    ]
)


result = establishments.aggregate([
    {
        "$project": {
            "longitude_type": { "$type": "$geocode.longitude" },
            "latitude_type": { "$type": "$geocode.latitude" }
        }
    }
])
