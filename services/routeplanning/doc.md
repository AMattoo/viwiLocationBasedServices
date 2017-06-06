<h3 style="text-align: center;">service definition: <i>viwi.service.routeplanning</i></h3>
<p style="text-align: center;">j3ss5t (GitHub)</p>

A service for planning and managing routes.

# Table of contents

* [General information](#General)
  * [Author](#Author)
  * [Contributors](#Contributors)

* [Resources](#Resources)
  * [/routeplanning/routePolicies/](#routeplanning.routePolicies)
  * [/routeplanning/routes/](#routeplanning.routes)

# <a name="General"></a>General information
**Version:** 0.0.1-pre-alpha+review

## <a name="Author"></a>Author
**Name:** Jonas Schmidt<br />
**GitHub:** j3ss5t &lt;j0n45@mailbox.org&gt;<br />
**Twitter:** @j3s_s5t

# <a name="Resources"></a>Resources

## <a name="routeplanning.routePolicies"></a>/routeplanning/routePolicies/

A resource used as source of potentially dynamic generated policies which can be supplied to routes. (e.g. time least, cost least, distance least, taking real traffic into account or not, etc.) This policies a influencing the route calculation in a specific way.

### <a name="routePolicyObject"></a>routePolicyObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |

### Resource level access (/routeplanning/routePolicies/)

#### GET


**Note**:
Use a http GET request on /routeplanning/routePolicies/ to retrieve a list of available elements of type [routePolicyObject](#routePolicyObject)

Subscribe to /routeplanning/routePolicies/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |

##### Request/response example

```lang-none
GET /routeplanning/routePolicies/ HTTP/1.1
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
      "uri": "/routeplanning/routePolicies/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/routeplanning/routePolicies/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```



## Element level access (/routeplanning/routePolicies/:*uuid*)
#### GET

**Note**:

Use a http GET request on /routeplanning/routePolicies/:*uuid* to retrieve a particular [routePolicyObject](#routePolicyObject)

Subscribe to /routeplanning/routePolicies/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /routeplanning/routePolicies/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
      "uri": "/routeplanning/routePolicies/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```




## Events
This endpoint will not send any events. Therefor you can not register for them.

## <a name="routeplanning.routes"></a>/routeplanning/routes/

A resource of elements representing a route. A route element is representation of a physical route.

### <a name="routeObject"></a>routeObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| alternatives                 | A specific number of alternative routes which are calculated by the service. (e.g. most efficient, fastest, etc.) | object        |               |               | [/routeplanning/routes/routeObject](#routeObject) |
| consumingTime                | The consuming time of the route. This should be a approximation. | string        | duration      |               | - |
| destination                  | The actual destination location given by the client.       | object        |               |               | [/locality/locations/locationObject](#locationObject) |
| distance                     | The distance of the calculated trip. See distance unit.    | number        |               |               | [0..inf]  |
| distanceUnit                 | The unit for the value: distance.                          | string        | distance      |               | - |
| origin                       | The origin location. Can be used to plan a specific route for e.g. demo mode. Default is the current vehicle position. (optional) | object        |               |               | [/locality/locations/locationObject](#locationObject) |
| path                         | This is the geometry of the calculated route.              | object        |               |               | [/cartography/geometries/geometryObject](#geometryObject) |
| policy                       | The applied policy given by the user. This will influence the route calculation in a specific way. Note that the service will (hopefully) check for plausibility. | array         |               |               | [/routeplanning/routePolicies/routePolicyObject](#routePolicyObject) |
| status                       | The status of the route. As soon as the client sets the destination location the service will start to calculate the route based on the current parameter set. | string        |               |               | idle<br />calculating<br />ready |
| type                         | The type of the route. The service will calculate different alternative routes. These routes will be of the type 'alternative'. | string        |               |               | alternative<br />original |
| viaPoints                    | The via points that should be considered while calculating the route. | object        |               |               | [/locality/locations/locationObject](#locationObject) |

### Resource level access (/routeplanning/routes/)

#### GET


**Note**:
Use a http GET request on /routeplanning/routes/ to retrieve a list of available elements of type [routeObject](#routeObject)

Subscribe to /routeplanning/routes/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |
| status                       | string        |               | no       |

##### Request/response example

```lang-none
GET /routeplanning/routes/ HTTP/1.1
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
      "uri": "/routeplanning/routes/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/routeplanning/routes/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```

#### POST


**Note**:
Use a http POST request on /routeplanning/routes/ to create a new element of type [routeObject](#routeObject)

Subscribe to /routeplanning/routes/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| destination                  | string        | uri           | no       |
| name                         | string        |               | no       |
| origin                       | string        | uri           | no       |
| policy                       | array         |               | no       |
| viaPoints                    | string        | uri           | no       |

##### Request/response example

```lang-none
POST /routeplanning/routes/ HTTP/1.1
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
Location: /routeplanning/routes/3901a278-ba17-44d6-9aef-f7ca67c04840


{
  "status": "ok"
}
```


## Element level access (/routeplanning/routes/:*uuid*)
#### DELETE

**Note**:

Use a http DELETE request on /routeplanning/routes/:*uuid* to update a particular [routeObject](#routeObject)

Subscribe to /routeplanning/routes/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| viaPoints                    | string        | no       |

##### Request/response example

```lang-none
DELETE /routeplanning/routes/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

Use a http GET request on /routeplanning/routes/:*uuid* to retrieve a particular [routeObject](#routeObject)

Subscribe to /routeplanning/routes/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /routeplanning/routes/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
      "uri": "/routeplanning/routes/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```



#### POST

**Note**:

Use a http POST request on /routeplanning/routes/:*uuid* to update a particular [routeObject](#routeObject)

Subscribe to /routeplanning/routes/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| viaPoints                    | string        | no       |

##### Request/response example

```lang-none
POST /routeplanning/routes/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

* /routeplanning/routes/ (resource level)
* /routeplanning/routes/:*uuid* (element level)
