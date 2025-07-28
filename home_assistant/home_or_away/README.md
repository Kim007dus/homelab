# Home or Away

To check whether I am home or not, I use two different `device.trackers`. I chose this approach because the GPS sensor from my Android phone was not always responsive, which caused some of my automations to be delayed or not work properly.

In the Companion App on my Android, I enabled the following sensors:

- `WIFI connection`
- `GPS`

## GPS Device Tracker

In Home Assistant, you can mark your house as 'home' on the `map`. This is then automatically used by your phone sensor. You can link this to a person via `Settings` > `People`, then click the person you want to assign it to. Under `Select the devices that belong to this person`, you can add your phone.

## WiFi Connected Device Tracker

This method of tracking your location is a bit more complex, but also more reliable: as soon as your phone connects to your WiFi, it will be marked as `home`. For this, you need MQTT. [More info here](https://www.home-assistant.io/integrations/mqtt). The installation is straightforward. Then, add the following line to your `configuration.yaml` using a file editor (I use the file editor add-on, but there are several options, [see here](https://www.home-assistant.io/common-tasks/os/)):

```yaml
mqtt: !include mqtt.yaml
```

I chose to add a small delay when the connection drops, so that if I just step outside to the mailbox or take out the trash, all automations (like turning off all the lights) don’t trigger immediately.

## YAML Files

- [Add device tracker to MQTT](mqtt.yaml)
- [WiFi connection](wifi_connection.yaml)
