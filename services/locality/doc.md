<h3 style="text-align: center;">service definition: <i>viwi.service.locality</i></h3>
<p style="text-align: center;">j3ss5t (GitHub)</p>

A service for managing localities. This includes searching for addresses and poi&#x27;s and getting further information of those places.

# Table of contents

* [General information](#General)
  * [Author](#Author)
  * [Contributors](#Contributors)

* [Resources](#Resources)
  * [/locality/locations/](#locality.locations)
  * [/locality/poiCategories/](#locality.poiCategories)
  * [/locality/searchResults/](#locality.searchResults)
  * [/locality/searches/](#locality.searches)

# <a name="General"></a>General information
**Version:** 0.0.1-pre-alpha+review

## <a name="Author"></a>Author
**Name:** Jonas Schmidt<br />
**GitHub:** j3ss5t &lt;j0n45@mailbox.org&gt;<br />
**Twitter:** @j3s_s5t

# <a name="Resources"></a>Resources

## <a name="locality.locations"></a>/locality/locations/

A resource for managing locations. This is used a representation of a physical location e.g. address, poi, wgs84 position.

### <a name="locationObject"></a>locationObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| city                         | The name of the actual city if available.                  | string        |               |               | - |
| country                      | The name of the actual country if available.               | string        |               |               | - |
| district                     | The name of the actual district if available.              | string        |               |               | - |
| geometry                     | The geometry of the locality e.g. borders.                 | object        |               |               | [/cartography/geometries/geometryObject](#geometryObject) |
| housenumber                  | The actual housenumber if available.                       | string        |               |               | - |
| language                     | The mainly spoken language in the locality.                | string        | language      |               | - |
| nameInLocalLanguage          | The main name of the locality in local language.           | string        |               |               | - |
| nearbyLocations              | The locations that are nearby. This might just be filled if this is a location found in a search. | array         |               |               | [/locality/locations/locationObject](#locationObject) |
| poiCategories                | The associate poi categories. Note that this will just be filled if the locality is a poi. | array         |               |               | [/locality/poiCategories/poiCategoryObject](#poiCategoryObject) |
| poiName                      | The actual name of a poi if available.                     | string        |               |               | - |
| position                     | The center position of the locality.                       | string        | geoposition   |               | - |
| postcode                     | The actual value of a post code if available.              | string        |               |               | - |
| rating                       | The rating of the locality if available. Note that this might just be filled if the locality is a poi. | number        |               | percent       | [0..100] |
| road                         | The actual name of a road if available.                    | string        |               |               | - |
| roadType                     | The type of the road.                                      | string        |               |               | - |
| state                        | The actual name of a state if available.                   | string        |               |               | - |
| telephone                    | The telephone number of the locality if available.         | string        | e164telephonenumber |               | - |

### Resource level access (/locality/locations/)

#### GET


**Note**:
Use a http GET request on /locality/locations/ to retrieve a list of available elements of type [locationObject](#locationObject)

Subscribe to /locality/locations/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |

##### Request/response example

```lang-none
GET /locality/locations/ HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


```

=>

```lang-none
HTTP/1.1 200 OK
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked


{
  "status": "ok",
  "data": [
    {
      "id": "3901a278-ba17-44d6-9aef-f7ca67c04840",
      "name": "lorem ipsum",
      "uri": "/locality/locations/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/locality/locations/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```



## Element level access (/locality/locations/:*uuid*)
#### GET

**Note**:

Use a http GET request on /locality/locations/:*uuid* to retrieve a particular [locationObject](#locationObject)

Subscribe to /locality/locations/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /locality/locations/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


```

```lang-none
HTTP/1.1 200 OK
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked


{
  "status": "ok",
  "data": [
    {
      "id": "3901a278-ba17-44d6-9aef-f7ca67c04840",
      "name": "lorem ipsum",
      "uri": "/locality/locations/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```




## Events
This endpoint will not send any events. Therefor you can not register for them.

## <a name="locality.poiCategories"></a>/locality/poiCategories/

A resource for potentially dynamic generated poi categories for localities.

### <a name="poiCategoryObject"></a>poiCategoryObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |

### Resource level access (/locality/poiCategories/)

#### GET


**Note**:
Use a http GET request on /locality/poiCategories/ to retrieve a list of available elements of type [poiCategoryObject](#poiCategoryObject)

Subscribe to /locality/poiCategories/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |

##### Request/response example

```lang-none
GET /locality/poiCategories/ HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


```

=>

```lang-none
HTTP/1.1 200 OK
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked


{
  "status": "ok",
  "data": [
    {
      "id": "3901a278-ba17-44d6-9aef-f7ca67c04840",
      "name": "lorem ipsum",
      "uri": "/locality/poiCategories/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/locality/poiCategories/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```



## Element level access (/locality/poiCategories/:*uuid*)
#### GET

**Note**:

Use a http GET request on /locality/poiCategories/:*uuid* to retrieve a particular [poiCategoryObject](#poiCategoryObject)

Subscribe to /locality/poiCategories/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /locality/poiCategories/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


```

```lang-none
HTTP/1.1 200 OK
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked


{
  "status": "ok",
  "data": [
    {
      "id": "3901a278-ba17-44d6-9aef-f7ca67c04840",
      "name": "lorem ipsum",
      "uri": "/locality/poiCategories/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```




## Events
This endpoint will not send any events. Therefor you can not register for them.

## <a name="locality.searchResults"></a>/locality/searchResults/

A resource for search results.

### <a name="searchResultObject"></a>searchResultObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| parent                       | The original search of the search result.                  | object        |               |               | [/places/searches/searchObject](#searchObject) |
| reference                    | The actual location that was found in the search.          | object        |               |               | [/locality/locations/locationObject](#locationObject) |

### Resource level access (/locality/searchResults/)

#### GET


**Note**:
Use a http GET request on /locality/searchResults/ to retrieve a list of available elements of type [searchResultObject](#searchResultObject)

Subscribe to /locality/searchResults/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| parent                       | string        | uri           | no       |

##### Request/response example

```lang-none
GET /locality/searchResults/ HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


```

=>

```lang-none
HTTP/1.1 200 OK
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked


{
  "status": "ok",
  "data": [
    {
      "id": "3901a278-ba17-44d6-9aef-f7ca67c04840",
      "name": "lorem ipsum",
      "uri": "/locality/searchResults/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/locality/searchResults/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```



## Element level access (/locality/searchResults/:*uuid*)
#### GET

**Note**:

Use a http GET request on /locality/searchResults/:*uuid* to retrieve a particular [searchResultObject](#searchResultObject)

Subscribe to /locality/searchResults/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /locality/searchResults/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


```

```lang-none
HTTP/1.1 200 OK
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked


{
  "status": "ok",
  "data": [
    {
      "id": "3901a278-ba17-44d6-9aef-f7ca67c04840",
      "name": "lorem ipsum",
      "uri": "/locality/searchResults/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```




## Events

The following events may be fired by client interaction or system side:

* /locality/searchResults/ (resource level)


## <a name="locality.searches"></a>/locality/searches/

A resource for creating and managing searches. These search elements are used for searching for localities e.g. address, poi, geo positions.

### <a name="searchObject"></a>searchObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| bounds                       | The bounding box in which (local) in the search will be perfomed. | object        |               |               | [/cartography/geometries/geometryObject](#geometryObject) |
| location                     | The center location to use for radius search.              | object        |               |               | [/locality/locations/locationObject](#locationObject) |
| needle                       | The actual string to search for.                           | string        |               |               | - |
| radius                       | The actual radius (distance) used for radius search. (optional) | number        |               |               | [0.01..inf] |
| radiusUnit                   | The unit for the value: radius. See radius.                | string        | distance      |               | - |
| results                      | The result set of the search.                              | array         |               |               | [/locality/searchResults/searchResultObject](#searchResultObject) |
| status                       | The status of the search. This property is used to start/stop a search or indicate that the search is complete. | string        |               |               | idle<br />running<br />complete |

### Resource level access (/locality/searches/)

#### POST


**Note**:
Use a http POST request on /locality/searches/ to create a new element of type [searchObject](#searchObject)

Subscribe to /locality/searches/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| location                     | string        | uri           | no       |
| name                         | string        |               | no       |
| needle                       | string        |               | no       |
| radius                       | number        |               | no       |
| status                       | string        |               | no       |

##### Request/response example

```lang-none
POST /locality/searches/ HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


{
  "viwi": "rockz.."
}
```

=>


```lang-none
HTTP/1.1 201 Created
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked
Location: /locality/searches/3901a278-ba17-44d6-9aef-f7ca67c04840


{
  "status": "ok"
}
```


## Element level access (/locality/searches/:*uuid*)
#### DELETE

**Note**:

Use a http DELETE request on /locality/searches/:*uuid* to update a particular [searchObject](#searchObject)

Subscribe to /locality/searches/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
DELETE /locality/searches/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


```



```lang-none
HTTP/1.1 201 Created
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked


{
  "status": "ok"
}
```

#### GET

**Note**:

Use a http GET request on /locality/searches/:*uuid* to retrieve a particular [searchObject](#searchObject)

Subscribe to /locality/searches/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /locality/searches/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


```

```lang-none
HTTP/1.1 200 OK
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked


{
  "status": "ok",
  "data": [
    {
      "id": "3901a278-ba17-44d6-9aef-f7ca67c04840",
      "name": "lorem ipsum",
      "uri": "/locality/searches/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```



#### POST

**Note**:

Use a http POST request on /locality/searches/:*uuid* to update a particular [searchObject](#searchObject)

Subscribe to /locality/searches/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| bounds                       | string        | no       |
| location                     | string        | no       |
| name                         | string        | no       |
| needle                       | string        | no       |
| radius                       | number        | no       |
| status                       | string        | no       |

##### Request/response example

```lang-none
POST /locality/searches/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
Host: 127.0.0.1:9000
Connection: keep-alive
Accept: application/json
User-Agent: Chrome/34.0.1847.137 Safari/537.36
Accept-Encoding: gzip,deflate
Accept-Language: en-US,en;q=0.8,de;q=0.6


{
  "viwi": "rockz.."
}
```


```lang-none
HTTP/1.1 201 Created
Vary: Accept-Encoding
Content-Type: application/json; charset=utf-8
ETag: "-32550834"
Content-Encoding: gzip
Date: Tue, 07 Apr 1980 00:00:00 GMT
Connection: keep-alive
Transfer-Encoding: chunked


{
  "status": "ok"
}
```



## Events

The following events may be fired by client interaction or system side:

* /locality/searches/:*uuid* (element level)
