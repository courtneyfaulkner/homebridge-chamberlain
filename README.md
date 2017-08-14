# homebridge-chamberlain

A Homebridge plugin for Chamberlain garage door openers with MyQ.

First set up your mychamberlain.com account, then add to your `config.json` in
the `accessories` array:

```json
{
  "accessory": "Chamberlain",
  "name": "Garage Door",
  "username": "your mychamberlain.com email",
  "password": "your mychamberlain.com password"
}
```

If you have multiple garage doors, the plugin will throw an error and list the controllable device IDs. Use those IDs to create individual accessories.

```json
{
  "accessory": "Chamberlain",
  "name": "Main Garage Door",
  "username": "your mychamberlain.com email",
  "password": "your mychamberlain.com password",
  "deviceId": "xxx"
},
{
  "accessory": "Chamberlain",
  "name": "Side Garage Door",
  "username": "your mychamberlain.com email",
  "password": "your mychamberlain.com password",
  "deviceId": "xxx"
},
...
```

To retrieve deviceIds, get a security token:

```
POST https://myqexternal.myqdevice.com/api/v4/User/Validate
User-Agent: Chamberlain/3773 (iPhone; iOS 10.0.1; Scale/2.00)
MyQApplicationId: OA9I/hgmPHFp9RYKJqCKfwnhh28uqLJzZ9KOJf1DXoo8N2XAaVX6A1wcLYyWsnnv
Content-Type: application/json
{
  "username": "xxx",
  "password": "xxx"
}
```

Use the security token to get a list of your devices, find the device with `MyQDeviceTypeName` = `GarageDoorOpener`, and use its `MyQDeviceId` as the deviceId in the config.json file.

```
GET https://myqexternal.myqdevice.com/api/v4/UserDeviceDetails/Get
User-Agent: Chamberlain/3773 (iPhone; iOS 10.0.1; Scale/2.00)
MyQApplicationId: OA9I/hgmPHFp9RYKJqCKfwnhh28uqLJzZ9KOJf1DXoo8N2XAaVX6A1wcLYyWsnnv
Content-Type: application/json
SecurityToken: xxx
```
