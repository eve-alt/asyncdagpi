# asyncdagpi
An async wrapper for http://dagpi.tk

[![Build Status](https://travis-ci.com/Daggy1234/asyncdagpi.svg?branch=master)](https://travis-ci.com/Daggy1234/asyncdagpi) [![License](https://img.shields.io/github/license/daggy1234/asyncdagpi)](https://mit-license.org/)  [![codestyle](https://img.shields.io/badge/code%20style-black-000000.svg)](https://pypi.org/project/black/) ![version](https://img.shields.io/pypi/v/asyncdagpi) ![python](https://img.shields.io/pypi/pyversions/asyncdagpi) 

## Documentation for asyncdagpi

### 1) Obtain a token

- - -
Join the discord server [here](https://server.daggy.tech) and verify yourself. Once done you can easily apply for a token via the process detailed.

### 2) Install the library

- - -

Use pip to install the library

```shell script
pip install asyncdagpi
```

### 3) Initialise the client

- - -

```python
from asyncdagpi import Client
API_CLIENT = Client('insert_your_token')
```

With this you should have a working API client that can help you authenticate and process api requests

### 4) Use One of the Features listed below with your client instance

- - -

- staticimage
- gif
- usertextimage
- textimage

These categories have a lot of features. A list of features can be found below or in the API documentation at 
[docs](https://dagpi.tk/docs)

You can use the client with a feature as follows:

```python
async def wanted(image_url:str):
    response = await API_CLIENT.staticimage('wanted',image_url)
```

### 5) Using the Response

- - -

The client returns an url as a default response. If the `bytes=True` parameter is passed then a BytesIO object is returned instead! The BytesIO response can be used in a lot of ways. Read the documentation here : [BytesIOdocs](https://docs.python.org/3/library/io.html) in the BytesIO section.

The examples below depict a few use cases

**Obtaining a url to share**

```python
async def wanted(image_url:str):
    response = await API_CLIENT.staticimage('wanted',image_url)
    return (response)
    
```

**Saving Response to file**

```python
async def wanted(image_url:str):
    response = await API_CLIENT.staticimage('wanted',image_url,bytes=True)
    with open('wanted.png''wb') as out:
        out.write(response.read())
```

**Opening The response with Pillow (PIL)**

```python
from PIL import Image
async def wanted(image_url:str):
    response = await API_CLIENT.staticimage('wanted',image_url,bytes=True)
    image = Image.open(response)
```

**Using the Discord.py library and sending response as a an image in an embed**

`please do remember to get a discord api token and run the bot using that.`

Get help with discord.py at [dpy server](https://discord.gg/dpy)

```python

import discord
from discord.ext import commands
bot = commands.Bot(command_prefix = '.')
@bot.command()
async def wanted(ctx,image_url:str):
    response = await API_CLIENT.staticimage('wanted',image_url)
    embed = discord.Embed(title='DAGPI image')
    embed.set_image(url=response)
    await ctx.send(embed=embed)  
```

### 6) Handling Exceptions

- - -
You can import exceptions from asyncdagpi.

```python
from asyncdagpi import exceptions
try:
    #request
except exceptions.ImageUnaccesible:
    print('No image at your url')
```
#### -  InvalidOption

This exception is raised when the feature chosen is not in the feature list ie. wanted is not a valid feature from the available options.

#### -  BadUrl

The api uses regex to validate urls. When an improper url is passed to the API this exception is raised

#### -  IncorrectToken

The token passed is invalid according to the api.

#### -  RateLimited

You are exceeding the maximum number of requests the api can take.

#### -  FileTooLarge

The file passed os too large for the API to process

#### -  APIError

The api raised an error. Issue with the API

#### -  ImageUnaccesible

The API was unable to find an image at your url within timeout and 

#### - UnkownError

This is when the API returns a non 200 code ie means an error occurred. This exception throws the status code along with a message explaining the status code. 

### Categories and their subsequent features

- - -

### staticimage

This returns an png image as an API url or (as BytesIO if `bytes=True`) and requires the image_url for a static image.

 ```python
API_CLIENT.staticimage(feature,image_url)

# feature - one of the features
# image_url - a static image url
```

Features:

- wanted
- evil
- bad
- hitler
- angel
- trash
- satan
- triggered
- obama
- hog
- ascii
- colors 
- rgbdata

### multiimage

This returns an png image as an API url or (as BytesIO if `bytes=True`) and requires the 2 image urls for the multiimage to be produced.

```python
API_CLIENT.multiimage(feature,image_url,second_image_url)
#feature: one of the features
#image_url url for first image
#second_image_url: url for image no2
```

Features:

- 5g1g
- whyareyougay

### Gif

Returns a gif as an API url or (as BytesIO if `bytes=True`) . Takes either  a static_image url or a gif url and returns a gif. Irrespective of the inupt output is always a gif.

 ```python
API_CLIENT.gif(feature,image_url)

# feature - one of the features
# image_url - a gif or static image_url
```

Features:

- paint
- solar
- blur
- invert
- pixel
- sepia
- deepfry
- wasted
- gay
- charcoal
- jail
- polaroid
- night

### usertextimage

Returns a png image as an API url or (as BytesIO if `bytes=True`). Takes in the following arguments

```python
API_CLIENT.usertextimage(feature,image_url,text,name)

# feature - one of the features
# image_url - a static image url
# text - the text the person will say
# name - the username that will be used for the person
```

Features:

- tweet
- quote (discord message)

#### textimage

Depending in the feature and imput either returns a static or gif image.
returns an API url or (as BytesIO if `bytes=True`)

```python
API_CLIENT.textimage(feature,image_url,text)

# feature - one of the features
# image_url - a static image url
# text - the text the person will say
```

Features:

- Thoughtimage: always returns a static response

