# FMS Event API
The event api allows pulling of match data almost immeadiatly after a match ends.

## Documentation
The endpoint documentation can be found [HERE](https://frcevents2.docs.apiary.io/#). **NOTE:** This api requires an API key and login.

## Obtaining an API key
To get your api key, create an account on [TeamForge](https://usfirst.collab.net/sf/projects/first_community_developers/). After creating and verifying your account, go back to the link and press the button on the left panel to request access to the poject. You must write a short paragraph detailing why you want access to the API. If your are approved, you will recieve an email from FIRST with your username and key at the bottom.

Your API key for HTTP access is created by adding your username to your key with a colon in the middle, then base64 encoding it. For example, if your username is `sampleuser` and your key is `7eaa6338-a097-4221-ac04-b6120fcc4d49` you would have this string:
```
sampleuser:7eaa6338-a097-4221-ac04-b6120fcc4d49
```

Bae64 encoding this would give:
```
c2FtcGxldXNlcjo3ZWFhNjMzOC1hMDk3LTQyMjEtYWMwNC1iNjEyMGZjYzRkNDk=
```