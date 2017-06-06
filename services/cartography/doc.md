<h3 style="text-align: center;">service definition: <i>viwi.service.cartography</i></h3>
<p style="text-align: center;">j3ss5t (GitHub)</p>

A service for controlling maps including the manipulation and management of layers, markers, cameras and custom elements.

# Table of contents

* [General information](#General)
  * [Author](#Author)
  * [Contributors](#Contributors)

* [Resources](#Resources)
  * [/cartography/geometries/](#cartography.geometries)
  * [/cartography/mapCameras/](#cartography.mapCameras)
  * [/cartography/mapDrawings/](#cartography.mapDrawings)
  * [/cartography/mapLayers/](#cartography.mapLayers)
  * [/cartography/mapMarkers/](#cartography.mapMarkers)
  * [/cartography/maps/](#cartography.maps)

# <a name="General"></a>General information
**Version:** 0.0.1-pre-alpha+review

## <a name="Author"></a>Author
**Name:** Jonas Schmidt
**GitHub:** j3ss5t &lt;j0n45@mailbox.org&gt;<br />
**Twitter:** @j3s_s5t

# <a name="Resources"></a>Resources

## <a name="cartography.geometries"></a>/cartography/geometries/

A resource for modeling geometries (e.g. line, point, polygon) with a list of shapepoints pointing to real world positions (WGS84).

### <a name="geometryObject"></a>geometryObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| color                        | The color of the geometry in case of a visual reprensentation. | string        | rgba          |               | - |
| shapepoints                  | The shapepoint of the geometry.                            | string        | geoposition   |               | - |
| type                         | The explicit type of the geometry.                         | string        |               |               | point<br />line<br />polygon |

### Resource level access (/cartography/geometries/)

#### POST


**Note**:
Use a http POST request on /cartography/geometries/ to create a new element of type [geometryObject](#geometryObject)

Subscribe to /cartography/geometries/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |
| color                        | string        | rgba          | no       |
| shapepoints                  | string        | geoposition   | yes      |
| type                         | string        |               | yes      |

##### Request/response example

```lang-none
POST /cartography/geometries/ HTTP/1.1
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
Location: /cartography/geometries/3901a278-ba17-44d6-9aef-f7ca67c04840


{
  "status": "ok"
}
```


## Element level access (/cartography/geometries/:*uuid*)
#### DELETE

**Note**:

Use a http DELETE request on /cartography/geometries/:*uuid* to update a particular [geometryObject](#geometryObject)

Subscribe to /cartography/geometries/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
DELETE /cartography/geometries/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

#### POST

**Note**:

Use a http POST request on /cartography/geometries/:*uuid* to update a particular [geometryObject](#geometryObject)

Subscribe to /cartography/geometries/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| color                        | string        | no       |

##### Request/response example

```lang-none
POST /cartography/geometries/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
This endpoint will not send any events. Therefor you can not register for them.

## <a name="cartography.mapCameras"></a>/cartography/mapCameras/

A resource for the representation and manipulation of a camera. A Camera is a device through which the user views the world.

### <a name="mapCameraObject"></a>mapCameraObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| zoomMode                     | The zoom mode of the camera. Might be auto like automatic zooming (e.g. animations or somehting) but can be either guide (e.g. route guidance) or manual. | string        |               |               | auto<br />guide<br />manual |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| center                       | The center position. Used for panning the map.             | string        | geoposition   |               | - |
| distancePerPixel             | The scale of a map in distance per pixel at the level of the target point. | number        |               |               | [0..inf] |
| distancePerPixelUnit         | The unit of the value: distance per pixel.                 | string        | distance      |               | - |
| focusedDrawings              | The visible drawings in the map the camera should zoom on and keep in focus. | object        |               |               | [/cartography/mapDrawings/mapDrawingObject](#mapDrawingObject) |
| orientation                  | The orientation angle of the camera in relation to the fixed point in degrees. See orientation mode. | number        |               | degree        | [0..359.999] |
| name                         | The specific name of an element                            | string        |               |               | - |
| targetPoint                  | The target point of a camera. Respectively the reference position on the map. | string        | geoposition   |               | - |
| tiltAngle                    | The tilt angle of the camera in degrees. See tilt mode.    | number        |               | degree        | [0..359.999] |
| tiltMode                     | Predefined tilt angles e.g. top and bird. Manual tilt mode enables the client to defined custom tilt angle. See tilt angle. | string        |               |               | top<br />bird<br />manual |
| zoomHeight                   | The actual height from the  camera to the target point.    | number        |               |               | [0..inf] |
| zoomHeightUnit               | The unit of the value: zoom height.                        | string        | distance      |               | - |
| zoomLevel                    | Predefined zoom levels that will be applied to the camera. Keep in mind that this value can be overwritten by a custom zoom height. | integer       |               |               | [0..1000] |
| orientationMode              | The fixed point of the camera. (e.g. north, guide, manual) | string        |               |               | north<br />guide<br />manual |

### Resource level access (/cartography/mapCameras/)

#### GET


**Note**:
Use a http GET request on /cartography/mapCameras/ to retrieve a list of available elements of type [mapCameraObject](#mapCameraObject)

Subscribe to /cartography/mapCameras/ to receive updates for element creations or removals from the collection.


##### Request/response example

```lang-none
GET /cartography/mapCameras/ HTTP/1.1
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
      "uri": "/cartography/mapCameras/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/cartography/mapCameras/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```



## Element level access (/cartography/mapCameras/:*uuid*)
#### GET

**Note**:

Use a http GET request on /cartography/mapCameras/:*uuid* to retrieve a particular [mapCameraObject](#mapCameraObject)

Subscribe to /cartography/mapCameras/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /cartography/mapCameras/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
      "uri": "/cartography/mapCameras/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```



#### POST

**Note**:

Use a http POST request on /cartography/mapCameras/:*uuid* to update a particular [mapCameraObject](#mapCameraObject)

Subscribe to /cartography/mapCameras/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| center                       | string        | no       |
| zoomMode                     | string        | no       |
| focusedDrawings              | string        | no       |
| name                         | string        | no       |
| orientation                  | number        | no       |
| orientationMode              | string        | no       |
| distancePerPixel             | number        | no       |
| tiltAngle                    | number        | no       |
| tiltMode                     | string        | no       |
| zoomHeight                   | number        | no       |
| zoomLevel                    | integer       | no       |
| targetPoint                  | string        | no       |

##### Request/response example

```lang-none
POST /cartography/mapCameras/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

* /cartography/mapCameras/:*uuid* (element level)


## <a name="cartography.mapDrawings"></a>/cartography/mapDrawings/

A resource for creating drawings that should be visible in the map.

### <a name="mapDrawingObject"></a>mapDrawingObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| reference                    | The actual element that be drawn.                          | object        |               |               | [/cartography/geometries/geometryObject](#geometryObject)<br />[/cartography/mapMarkers/mapMarkerObject](#mapMarkerObject)<br />[/routeplanning/routes/routeObject](#routeObject) |
| target                       | The target map of the drawing. See drawings in maps.       | object        |               |               | [/cartography/maps/mapObject](#mapObject) |
| visible                      | A flag for making the drawing visible or invisible to the user. | boolean       |               |               | - |

### Resource level access (/cartography/mapDrawings/)

#### GET


**Note**:
Use a http GET request on /cartography/mapDrawings/ to retrieve a list of available elements of type [mapDrawingObject](#mapDrawingObject)

Subscribe to /cartography/mapDrawings/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |
| target                       | string        | uri           | no       |
| visible                      | boolean       |               | no       |

##### Request/response example

```lang-none
GET /cartography/mapDrawings/ HTTP/1.1
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
      "uri": "/cartography/mapDrawings/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/cartography/mapDrawings/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```

#### POST


**Note**:
Use a http POST request on /cartography/mapDrawings/ to create a new element of type [mapDrawingObject](#mapDrawingObject)

Subscribe to /cartography/mapDrawings/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | yes      |
| reference                    | string        | uri           | yes      |
| target                       | string        | uri           | yes      |
| visible                      | boolean       |               | no       |

##### Request/response example

```lang-none
POST /cartography/mapDrawings/ HTTP/1.1
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
Location: /cartography/mapDrawings/3901a278-ba17-44d6-9aef-f7ca67c04840


{
  "status": "ok"
}
```


## Element level access (/cartography/mapDrawings/:*uuid*)
#### DELETE

**Note**:

Use a http DELETE request on /cartography/mapDrawings/:*uuid* to update a particular [mapDrawingObject](#mapDrawingObject)

Subscribe to /cartography/mapDrawings/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
DELETE /cartography/mapDrawings/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

Use a http GET request on /cartography/mapDrawings/:*uuid* to retrieve a particular [mapDrawingObject](#mapDrawingObject)

Subscribe to /cartography/mapDrawings/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /cartography/mapDrawings/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
      "uri": "/cartography/mapDrawings/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```



#### POST

**Note**:

Use a http POST request on /cartography/mapDrawings/:*uuid* to update a particular [mapDrawingObject](#mapDrawingObject)

Subscribe to /cartography/mapDrawings/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| visible                      | boolean       | no       |

##### Request/response example

```lang-none
POST /cartography/mapDrawings/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

* /cartography/mapDrawings/ (resource level)


## <a name="cartography.mapLayers"></a>/cartography/mapLayers/

A resource for the representation of map layers. This feature is seperated in a resource to support dynamically added or removed maps layers in runtime.

### <a name="mapLayerObject"></a>mapLayerObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |

### Resource level access (/cartography/mapLayers/)

#### GET


**Note**:
Use a http GET request on /cartography/mapLayers/ to retrieve a list of available elements of type [mapLayerObject](#mapLayerObject)

Subscribe to /cartography/mapLayers/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |

##### Request/response example

```lang-none
GET /cartography/mapLayers/ HTTP/1.1
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
      "uri": "/cartography/mapLayers/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/cartography/mapLayers/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```



## Element level access (/cartography/mapLayers/:*uuid*)
#### GET

**Note**:

Use a http GET request on /cartography/mapLayers/:*uuid* to retrieve a particular [mapLayerObject](#mapLayerObject)

Subscribe to /cartography/mapLayers/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /cartography/mapLayers/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
      "uri": "/cartography/mapLayers/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```




## Events
This endpoint will not send any events. Therefor you can not register for them.

## <a name="cartography.mapMarkers"></a>/cartography/mapMarkers/

A resource for the representation of map markers. (e.g. pins, pointers)

### <a name="mapMarkerObject"></a>mapMarkerObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| image                        | The actual image that should be shown.                     | string        | uri           |               | - |
| position                     | The target position of the marker in the map.              | object        |               |               | [/locality/locations/locationObject](#locationObject) |
| rotation                     | The rotation of the marker in degrees. See rotation orientation of the map. | number        |               | degree        | [0..359.999] |
| scaleFactor                  | The scaling factor of the maker.                           | number        |               |               | [0.01..1] |
| tiltAngle                    | The tilt angle of the marker in degrees. Don't really know if that's reasonable. | number        |               | degree        | [0..359.999] |

### Resource level access (/cartography/mapMarkers/)

#### POST


**Note**:
Use a http POST request on /cartography/mapMarkers/ to create a new element of type [mapMarkerObject](#mapMarkerObject)

Subscribe to /cartography/mapMarkers/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |
| image                        | string        | uri           | no       |
| position                     | string        | uri           | no       |
| rotation                     | number        |               | no       |
| scaleFactor                  | number        |               | no       |
| tiltAngle                    | number        |               | no       |

##### Request/response example

```lang-none
POST /cartography/mapMarkers/ HTTP/1.1
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
Location: /cartography/mapMarkers/3901a278-ba17-44d6-9aef-f7ca67c04840


{
  "status": "ok"
}
```


## Element level access (/cartography/mapMarkers/:*uuid*)
#### DELETE

**Note**:

Use a http DELETE request on /cartography/mapMarkers/:*uuid* to update a particular [mapMarkerObject](#mapMarkerObject)

Subscribe to /cartography/mapMarkers/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
DELETE /cartography/mapMarkers/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

Use a http GET request on /cartography/mapMarkers/:*uuid* to retrieve a particular [mapMarkerObject](#mapMarkerObject)

Subscribe to /cartography/mapMarkers/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /cartography/mapMarkers/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
      "uri": "/cartography/mapMarkers/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```



#### POST

**Note**:

Use a http POST request on /cartography/mapMarkers/:*uuid* to update a particular [mapMarkerObject](#mapMarkerObject)

Subscribe to /cartography/mapMarkers/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| position                     | string        | no       |
| rotation                     | number        | no       |
| scaleFactor                  | number        | no       |
| tiltAngle                    | number        | no       |

##### Request/response example

```lang-none
POST /cartography/mapMarkers/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

* /cartography/mapMarkers/:*uuid* (element level)


## <a name="cartography.maps"></a>/cartography/maps/

A resource for the representation and manipulation of a some kind of visual map.

### <a name="mapObject"></a>mapObject


#### Properties

| name                         | description                                                | type          | format        | unit(s)       | value(s)              |
|------------------------------|------------------------------------------------------------|---------------|---------------|---------------|-----------------------|
| id                           | The unique identifier for an element.                      | string        | uuid          |               | - |
| name                         | The specific name of an element                            | string        |               |               | - |
| uri                          | The unique uniform resource (respectively element) identifier. | string        | uri           |               | - |
| camera                       | The primary active camera which should be used for generating the perspective of the target map. | object        |               |               | [/cartography/mapCameras/mapCameraObject](#mapCameraObject) |
| drawings                     | The representation of all drawings which are targeted to the map. These drawings should be visible in the map as long as they are marked as visible. (read-only) | array         |               |               | [/cartography/mapDrawings/mapDrawingObject](#mapDrawingObject) |
| layers                       | The list of active layers of the map. There might be more than one. (e.g. traffic and real view) | array         |               |               | [/cartography/mapLayers/mapLayerObject](#mapLayerObject) |
| mode                         | The mode (e.g. 2D, 3D) of the map.                         | string        |               |               | 2d<br />3d |

### Resource level access (/cartography/maps/)

#### GET


**Note**:
Use a http GET request on /cartography/maps/ to retrieve a list of available elements of type [mapObject](#mapObject)

Subscribe to /cartography/maps/ to receive updates for element creations or removals from the collection.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | format         | mandatory |
|------------------------------|---------------|---------------|-----------|
| name                         | string        |               | no       |

##### Request/response example

```lang-none
GET /cartography/maps/ HTTP/1.1
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
      "uri": "/cartography/maps/3901a278-ba17-44d6-9aef-f7ca67c04840"
    },
    {
      "id": "8901870-b526-11e3-a5e2-0800200c9a66",
      "name": "dolor sit",
      "uri": "/cartography/maps/8901870-b526-11e3-a5e2-0800200c9a66"
    }
  ]
}
```



## Element level access (/cartography/maps/:*uuid*)
#### GET

**Note**:

Use a http GET request on /cartography/maps/:*uuid* to retrieve a particular [mapObject](#mapObject)

Subscribe to /cartography/maps/:*uuid* to receive updates on element level changes.


##### Request/response example

```lang-none
GET /cartography/maps/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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
      "uri": "/cartography/maps/3901a278-ba17-44d6-9aef-f7ca67c04840"
    }
  ]
}
```



#### POST

**Note**:

Use a http POST request on /cartography/maps/:*uuid* to update a particular [mapObject](#mapObject)

Subscribe to /cartography/maps/:*uuid* to receive updates on element level changes.

##### Request parameters

The following parameters can be used with the request and subscriptions:

| name                         | type          | mandatory |
|------------------------------|---------------|-----------|
| camera                       | string        | no       |
| layers                       | array         | no       |
| mode                         | string        | no       |

##### Request/response example

```lang-none
POST /cartography/maps/3901a278-ba17-44d6-9aef-f7ca67c04840 HTTP/1.1
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

* /cartography/maps/:*uuid* (element level)
