# ThreatWindsPythonSDK

_ThreatWindsPythonSDK is a set of tools that allow interaction with ThreatWinds API. This SDK has functions to obtain information about active threats, and at the same time add new threats_

## Getting started
_You must create in the root of your project an .env file that will contain the api-key and the api-secret of the ThreatWinds API. You should define them with the names TW_API_KEY and TW_API_SECRET._

### Requirements

Python 3.7+
requests 2.28.1
python-dotenv 0.21.0

_For install the requirements:_

```
pip install -r requirements.txt

```

_or:_

```
python -m pip install requests
python -m pip install python-dotenv
```

## Deploy

_You should be aware that these functions return two values. The first **response** value will save the response if the request was successful. If it was not successful, it will be the value None. The second value **code**, will be the response code received. In case there is a connection problem, this second value will be 0_

### Function sent_entities

_For insert new entities, you need to call the following function. If the request is correct, the first value received **response** will be an acknowledged message:_

```
response, code = pythreatwinds_sdk.sent_entities(new_entities)
```

Where new_entities must be a list of objects in the following format:

```
[
  {
        "type": "malware",
        "value": "Dridex",
        "reputation": -3,
        "attributes": [],
        "associations": [
            {
                "name": "",
                "comment":"",
                "entity":{
                    "type": "ip",
                    "value": "51.178.161.32",
                    "reputation": -3,
                    "attributes":[],
                    "associations":[]
                }
            }
        ]
    }
]
```

### Function sent_associations

_For insert new associations, you need to call the following function. If the request is correct, the first value received **response** will be an acknowledged message:_

```
response, code = pythreatwinds_sdk.sent_associations(new_associations)
```

Where new_associations must be a objects in the following format:

```
{
  "associations": [
    "b97f454d-afad-421b-b157-38cda7d0b612", 
    "22721539-0471-440b-829e-069a9cdcc6ae"
  ],
  "comment": "Any important comment about the association"
}
```

### Function get_def_entities

_For request entity definitions, you need to call the following function. If the request is correct, the first value received **response** will be a list of entity definitions:_

```
response, code = pythreatwinds_sdk.get_def_entities()
```

### Function get_entities_search

_For find a list of entities containing a string, you must call to the following function. If the request is correct, the first value received **response** will be a list of the entities found:_
```
response, code = pythreatwinds_sdk.get_entities_search(value, limit, offset)
```

_Must be passed as arguments:_
    -value: Must be a string that will be searched.If you don't have quotes, it will be searched as independent words, only elements that contain all the words will be returned. The order of the words doesn't matter. If it is enclosed in quotes: it will be searched as a complete phrase, only elements that contain all the words in the exact order will be returned. The word "or" works like the OR operator in a programming language. The words or, and, the, he, she, it, etc. are not taken into account as search parameters. A hyphen works like the negation operator in a programming language.
    -limit: Must be an integer>0. Default 50. Is optional
    -offset: Must be an integer>=0. Default 0. Is optional

  ### Function get_entities_type

_For find a list of entities of some type, you must call the following function. If the request is correct, the first value received **response** will be a list of the entities found:_
```
response, code = pythreatwinds_sdk.get_entities_type(value, limit, offset, reputation, accuracy, lsa)
```

_Must be passed as arguments:_
    -value: entity type.Must be a string. Consult **Function get_def_entities**
    -limit: Must be an integer>0. Default 50. Is optional
    -offset: Must be an integer>=0. Default 0. Is optional
    -reputation: Must be any, bad or good. Default bad. Is optional
    -accuracy: Must be an integer betwen o to 3. Default 0. Is optional
    -lsa: Must be a timestamp in seconds since Unix(UTC) or a relative time like now-15m, now-30m, now-1h, now-8h, now-24h, now-7d, now-30d, now-90d or now-120d. Default now-24h. Is optional

### Function get_entity_id

_For find an entity with an id, you must call to the following function. If the request is correct, the first value received **response** will be the entity found:_
```
response, code = pythreatwinds_sdk.get_entity_id(value, limit, offset)
```

_Must be passed as arguments:_
    -value: Entity ID. Must be a string
    -limit: Must be an integer>0. Default 50. Is optional
    -offset: Must be an integer>=0. Default 0. Is optional

### Function get_entity_value

_For find an entity with an value, you must call to the following function. If the request is correct, the first value received **response** will be the entity found:_
```
response, code = pythreatwinds_sdk.get_entity_value(value, limit, offset)
```

_Must be passed as arguments:_
    -value: Entity value. Must be a string
    -limit: Must be an integer>0. Default 50. Is optional
    -offset: Must be an integer>=0. Default 0. Is optional

### Function sent_geoip_location

_For sent a new location, you need to call the following function. If the request is correct, the first value received **response** will be message acknowledged:_

```
response, code = pythreatwinds_sdk.sent_geoip_location(new_location)
```

Where new_location must be an object with the following format:

```
{
  "accuracyRadius": 100,
  "city": "Canberra",
  "country": "Australia",
  "countryCode": "AU",
  "latitude": 453.334,
  "longitude": -453.334,
  "segment": "1.1.1.0/24"
}
```

### Function get_geoip_location

_For find the geolocation of the given IP, you must call to the following function. If the request is correct, the first value received **response** will be the geolocation found:_
```
response, code = pythreatwinds_sdk.get_geoip_location(ip)
```

_Must be passed as arguments:_
    -ip: IP address. Must be a string

### Function sent_geoip_organization

_For sent a new organization, you need to call the following function. If the request is correct, the first value received **response** will be message acknowledged:_

```
response, code = pythreatwinds_sdk.sent_geoip_organization(new_organization)
```

Where new_location must be an object with the following format:

```
{
  "asn": 353453,
  "aso": "CloudFlare INC",
  "segment": "1.1.1.0/24"
}
```

### Function get_geoip_organization

_For find the organization of the given IP, you must call to the following function. If the request is correct, the first value received **response** will be the organization found:_
```
response, code = pythreatwinds_sdk.get_geoip_organization(ip)
```

_Must be passed as arguments:_
    -ip: IP address. Must be a string

## Running tests
If you want to get a demo of how functions work, some test functions with default values ​​have been developed, which you can call by simply adding the phrase _test to the name of the function you want to test. The following example shows how to call the function to test sent_entities:

```
sent_entities_test()
```

## Licence
_This project is under MIT Licence_