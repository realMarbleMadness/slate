---
title: Box2D Optimizer

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python

toc_footers:
  - <a href='https://github.com/realMarbleMadness/Box2D'>Box2D repository</a>

search: true
---

# Introduction

For more detailed explanation of this optimizer, refer to [upstream's REAMDE written by Leo and Alex](https://github.com/leonidk/Box2D/blob/master/README.md). This one is a simplified version.

# Install, Build and Run

## Install dependencies

Create a virtual environment of Python3. Python2 is not capatible since [Unpacking Argument Lists](https://docs.python.org/3/tutorial/controlflow.html#unpacking-argument-lists) is not available in Python2. How to create a virtual environment? It's 1:30 a.m. and I'm too tired. just search on Google and learn something.

> To install python dependencies, use this code:

```shell
pip install -r requirements.txt
```

```python
# It can't be
```

## Build

> To build C++ code, run this

```shell
./premake5 gmake
cd Build/gmake/
make -j -l config=release
```

```python
# It can't be
```

## Run

> To spin up the API server, run this

```shell
python server.py
```

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
        "x": 10,
        "y": 10.5
    },
    "bounds": {
        "x": [
            -40,
            20
        ],
        "y": [
            0,
            40
        ],
        "rotation": [
            0,
            31.4159265359
        ]
    },
    "n_obstacles": 3,
    "obstacles": [
        {
            "width": 4.0,
            "height": 0.8,
            "x": -9.236634994986835,
            "y": 18.80205961937183,
            "rotation": 15.12052944790599
        },
        {
            "width": 4.0,
            "height": 0.8,
            "x": -7.696743695787747,
            "y": 18.07787349775663,
            "rotation": 13.93119631927455
        },
        {
            "width": 4.0,
            "height": 0.8,
            "x": -10.06786265843493,
            "y": 18.43501197009068,
            "rotation": 13.937406748489341
        }
    ]
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

# Q&A

## Why don't use ROS to communicate?

Because ROS Kinetic does not support Python3.