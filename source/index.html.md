---
title: Box2D Optimizer

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python

toc_footers:
  - <a href='https://github.com/realMarbleMadness/Box2D'>Box2D repository</a>

search: true
---

# Get Block Poses

> To get pose, use this code:

```python
# Install requests first, i.e. pip install requests
import requests
testData = {
    "destination": {
        "x": 0.6,
        "y": 0.2,
        "width": 0.15,
        "height": 0.1
    },
    "bounds": {
        "x": [-0.8, 0.8],
        "y": [0, 1.6],
        "rotation": [0, 31.4159265359]
    },
    "n_obstacles": 3,
    "obstacles": [
        {"width": 0.05, "height": 0.24},
        {"width": 0.05, "height": 0.24},
        {"width": 0.05, "height": 0.24}
    ],
    "ball": {
        "radius": 0.01,
        "location": [-0.6, 1.5],
        "linear_velocity": [0.3, -0.1]
    }
}
r = requests.post('http://localhost:5000/getpose', json=testData)
r.json()
```

```shell
# With shell, you can just pass the correct header with each request
curl -H "Content-Type: application/json" -X POST -d '{"destination":{"x":0.6,"y":0.2,"width":0.15,"height":0.1},"bounds":{"x":[-0.8,0.8],"y":[0,1.6],"rotation":[0,31.4159265359]},"n_obstacles":3,"obstacles":[{"width":0.05,"height":0.24},{"width":0.05,"height":0.24},{"width":0.05,"height":0.24}],"ball":{"radius":0.01,"location":[-0.6,1.5],"linear_velocity":[0.3,-0.1]}}' http://localhost:5000/getpose
```
> The above command returns JSON structured like this:

```json
{
    "destination": {
        "x": 0.6,
        "y": 0.2,
        "width": 0.15,
        "height": 0.1
    },
    "bounds": {
        "x": [
            -0.8,
            0.8
        ],
        "y": [
            0,
            1.6
        ],
        "rotation": [
            0,
            31.4159265359
        ]
    },
    "n_obstacles": 3,
    "obstacles": [
        {
            "width": 0.05,
            "height": 0.24,
            "x": -0.5588995672175655,
            "y": 1.1043541047952923,
            "rotation": 13.823030632598789
        },
        {
            "width": 0.05,
            "height": 0.24,
            "x": 0.6686917139357296,
            "y": 0.6793950132973555,
            "rotation": 18.732470832091693
        },
        {
            "width": 0.05,
            "height": 0.24,
            "x": -0.02703522727968692,
            "y": 0.5507303787450926,
            "rotation": 7.6811874823266315
        }
    ],
    "ball": {
        "radius": 0.01,
        "location": [
            -0.6,
            1.5
        ],
        "linear_velocity": [
            0.3,
            -0.1
        ]
    }
}
```

This endpoint retrieves the poses.

### HTTP Request

`POST http://localhost:5000/getpose`

#### Header

Key | Value
--------- | -------
Content-Type | application/json

#### Body

The body of POST should be a raw JSON string, see Python code for example data.

<aside class="notice">
Expect about 40 seconds to get answer.
</aside>

# Visualize

> To visualize on Mac, use this code:

```python
# Install requests first, i.e. pip install requests
import requests
r = requests.post('http://localhost:5000/visualize', json=optimizedEnv)
r.json()
```

```shell
curl -H "Content-Type: application/json" -X POST -d '{"destination":{"x":0.6,"y":0.2,"width":0.15,"height":0.1},"bounds":{"x":[-0.8,0.8],"y":[0,1.6],"rotation":[0,31.4159265359]},"n_obstacles":3,"obstacles":[{"width":0.05,"height":0.24,"x":-0.5588995672175655,"y":1.1043541047952923,"rotation":13.823030632598789},{"width":0.05,"height":0.24,"x":0.6686917139357296,"y":0.6793950132973555,"rotation":18.732470832091693},{"width":0.05,"height":0.24,"x":-0.02703522727968692,"y":0.5507303787450926,"rotation":7.6811874823266315}],"ball":{"radius":0.01,"location":[-0.6,1.5],"linear_velocity":[0.3,-0.1]}}' http://localhost:5000/visualize
```

This endpoint render the simulation in host machine (Mac).

### HTTP Request

`POST http://localhost:5000/visualize`

#### Header

Key | Value
--------- | -------
Content-Type | application/json

#### Body

The body of POST should be a raw JSON string, see Shell code for example data.

# Q&A

## Why don't use ROS to communicate?

Because ROS Kinetic does not support Python3.