&nbsp;

<h3 style="text-align: center;">service definition: <i>viwi.service.routeguidance</i></h3>
<p style="text-align: center;">j3ss5t (GitHub)</p>
<p>&nbsp;</p>

The service acts as a source for positioning data and is meant to be used for managing route guidance.

# Table of contents

* [General information](#General)
  * [Author](#Author)
  * [Contributors](#Contributors)
* [Changelog](#Changelog)
* [Resources](#Resources)
  * [/routeguidance/guides/](#routeguidance.guides)
  * [/routeguidance/positionings/](#routeguidance.positionings)

# <a name="General"></a>General information
version: 0.0.1

## <a name="Author"></a>Author
**GitHub:** j3ss5t &lt;j0n45@mailbox.org&gt;<br />
**Twitter:** @j3s_s5t

# <a name="Resources"></a>Resources

## <a name="routeguidance.guides"></a>/routeguidance/guides/

A resource of elements which are representing entities of navigation guidances. These elements are used for starting/stopping a route guidance based on a precaclulated route.

### <a name="guideObject"></a>guideObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| positioning                  | The target positioning. This is used to parameterize the positioning which should be used while route guidance is active. There might be more than one source of positioning infomation. (e.g. demo positioning) | object        |               |               | [/routeguidance/positionings/positioningObject](#positioningObject) |
| route                        | The target route. The actual route for the route guidance. Based on the fact that a route is the representation of a physical route the route guidance entity has to store infomation about e.g. how much of the route is already done respectivly how much of the way to the destination is left. See route. | object        |               |               | [/routeplanning/routes/routeObject](#routeObject) |
| status                       | The actual status of a route guidance. This is representing the status of a route guidance and is used for starting/stopping a route guidance. | string        |               |               | idle<br />guiding |

### Resource level access (/routeguidance/guides/)

#### GET


**Note**:
Use a http GET request on /routeguidance/guides/ to retrieve a list of available elements of type [guideObject](#guideObject)

Subscribe to /routeguidance/guides/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |

##### Request/response example

```lang-none
GET /routeguidance/guides/ HTTP/1.1
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
      "uri": "/routeguidance/guides/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/routeguidance/guides/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```



## Element level access (/routeguidance/guides/:*uuid*)
#### DELETE

**Note**:

Use a http DELETE request on /routeguidance/guides/:*uuid* to update a particular [guideObject](#guideObject)

Subscribe to /routeguidance/guides/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| route                        | string        | no       |

##### Request/response example

```lang-none
DELETE /routeguidance/guides/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

Use a http GET request on /routeguidance/guides/:*uuid* to retrieve a particular [guideObject](#guideObject)

Subscribe to /routeguidance/guides/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /routeguidance/guides/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
      "uri": "/routeguidance/guides/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```



#### POST

**Note**:

Use a http POST request on /routeguidance/guides/:*uuid* to update a particular [guideObject](#guideObject)

Subscribe to /routeguidance/guides/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| positioning                  | string        | no       |
| route                        | string        | no       |
| status                       | string        | no       |

##### Request/response example

```lang-none
POST /routeguidance/guides/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

* /routeguidance/guides/:*uuid* (element level)


## <a name="routeguidance.positionings"></a>/routeguidance/positionings/

A resource which is used for the representation of positioning entities. This might be something like gps receivers or demo mode positioning sources.

### <a name="positioningObject"></a>positioningObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| heading                      | The heading of the positioning in degress.                 | number        |               | degree        | [0..359.999] |
| mapMatchedLocation           | The position which is already map matched.                 | object        |               |               | [/locality/locations/locationObject](#locationObject) |
| rawLocation                  | The position which is not matched to anything.             | string        | geoposition   |               | - |
| speed                        | The speed of the positioning. See speed unit.              | number        |               |               | [0..10000] |
| speedUnit                    | The unit of the value: speed. See speed.                   | string        | speed         |               | - |
| time                         | The current time given by the positioning.                 | string        | time          |               | - |
| usedSatellites               | The number of used satellites. Note that this is just available if the positioning source is a GPS. | integer       |               |               | [0..1000] |
| visibleSatellites            | The number of visible satellites. Note that this is just available if the positioning source is a GPS. | integer       |               |               | [0..10000] |

### Resource level access (/routeguidance/positionings/)

#### GET


**Note**:
Use a http GET request on /routeguidance/positionings/ to retrieve a list of available elements of type [positioningObject](#positioningObject)

Subscribe to /routeguidance/positionings/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |

##### Request/response example

```lang-none
GET /routeguidance/positionings/ HTTP/1.1
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
      "uri": "/routeguidance/positionings/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/routeguidance/positionings/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```



## Element level access (/routeguidance/positionings/:*uuid*)
#### GET

**Note**:

Use a http GET request on /routeguidance/positionings/:*uuid* to retrieve a particular [positioningObject](#positioningObject)

Subscribe to /routeguidance/positionings/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /routeguidance/positionings/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
      "uri": "/routeguidance/positionings/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```




## Events

The following events may be fired by client interaction or system side:

* /routeguidance/positionings/:*uuid* (element level)
