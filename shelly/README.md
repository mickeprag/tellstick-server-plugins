# Shelly plugin för Telldus Tellstick
Shelly plugin for Telldus Tellstick Net/ZNet v1/v2 (white box, Net,ZNet v1, v2)

Shelly devices will show as a device in Telldus Live and mobile app. It
support on/off, dimming, rgb, sensors (power, temp etc)

## Supported devices
- Shelly 1
- Shelly 1PM
- Shelly 2
- Shelly 2.5
- Shelly 4 PRO
- Shelly RGBWW
- Shelly LED
- Shelly RGBW2
- Shelly H&T
- Shelly FLOOD
- Shelly PLUG
- Shelly PLUG S
- Shelly DIMMER
- Shelly DIMMER/SL

Only for firmware < 1.8.x, new release comming soon.

## Requirement
This plugin need Tellstick version 1.3.1. This version is currently in beta and you need to switch to beta under settings on your Tellstick.

## Installation
[Se wiki pages (only swedish)](https://github.com/StyraHem/tellstick-server-plugins/wiki/Shelly-plugin-f%C3%B6r-Telldus-Tellstick)

## Screen shots
![Screenshot](https://raw.githubusercontent.com/StyraHem/tellstick-server-plugins/master/shelly/img/screencapture1.png)

## Example of Lua comamnds
```lua
-- File: TestShelly.lua
local deviceName = "Shelly1" -- Name of your Shelly device
local deviceManager = require "telldus.DeviceManager"

function onInit()
	print("onInit")
	local device = deviceManager:findByName(deviceName)

	if device == nil then
		print("Could not find the device %s", deviceName)
		return
	end

	--Here you can do command on your device, see below
	device:turnon()
end 
```
### Shelly 1, Shelly 2, Shelly 4, Shelly PLUG
```lua
--On and off
device:turnon()
device:turnoff()
```
### Shelly 2, roller mode
```lua
--Roller
device:up()
device:down()
device:stop()
```
### Shelly Bulb, Shelly RGBWW, Shelly RGBW2
```lua
--On and off
device:turnon()
device:turnoff()

--Dim
device:command("dim", 255) --Full brightness
device:command("dim", 5)	 --Low brightness
device:setDim(255) --Full brightness
device:setDim(5) --Low brightness

--White mode
device:command("rgb", 0x1000000 + 6500) --White 6500K
device:command("rgb", 0x1000000 + 3000) --White 3000K
device.setWhite() -- switch to white mode
device.setWhite(6500) -- switch to white mode, 6500K
device.setWhite(3500, 255/2 ) -- switch to white mode, 3500K, half brightness

--RGB mode
device:command("rgb", 0xFF0000) --Red
device:command("rgb", 0x00FF00) --Green
device:command("rgb", 0x0000FF) --Blue'
device:setRgb( 0xFF, 0, 0 ) -- Red
device:setRgb( 0, 255, 0 , 255/2 ) -- Green, half brightness

--Effects
device:command("rgb", 0x2000000 + 0) --No effect
device:command("rgb", 0x2000000 + 1) --meteor shower
device:command("rgb", 0x2000000 + 2) --gradual change
device:command("rgb", 0x2000000 + 3) --breath
device:command("rgb", 0x2000000 + 4) --flash
device:command("rgb", 0x2000000 + 5) --on/off gradual
device:command("rgb", 0x2000000 + 6) --red/green flash
device:setEffect(0) --No effect
device:setEffect(6) --red/green flash
```
