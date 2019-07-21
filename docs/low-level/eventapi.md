---
layout: default
title: "Events API"
parent: "Low Level"
permalink: /docs/lowlevel/eventsapi
authors: ['ewpratten']
---

# FMS Event API
The event api allows pulling of match data almost immeadiatly after a match ends.

## Documentation
The endpoint documentation can be found [HERE](https://frcevents2.docs.apiary.io/#). **NOTE:** This api requires an API key and login.

## Obtaining an API key
To get your api key, head over to the new request site [https://frc-events.firstinspires.org/services/API](https://frc-events.firstinspires.org/services/API) and request a token. Make sure to list 5024 as your frc team.

Your API key for HTTP access is created by adding your username to your key with a colon in the middle, then base64 encoding it. For example, if your username is `sampleuser` and your key is `7eaa6338-a097-4221-ac04-b6120fcc4d49` you would have this string:
```
sampleuser:7eaa6338-a097-4221-ac04-b6120fcc4d49
```

Bae64 encoding this would give:
```
c2FtcGxldXNlcjo3ZWFhNjMzOC1hMDk3LTQyMjEtYWMwNC1iNjEyMGZjYzRkNDk=
```

## Wrapper APIs
While nobody talks about the event api, you have seen it used before under a different name. **The Blue Alliance API** is actually just a wrapper around the Events API. The only difference is that The Blue Alliance uses a Docker caching server (This is why the TBA app is always slightly out of date during an event).

I ([@ewpratten](https://github.com/ewpratten)) also have my own wrapper at [api.retrylife.ca](https://api.retrylife.ca/frc) that allows for limited polling of the API.
