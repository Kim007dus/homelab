# Bedtime Automation

I've created automations for all my bedtime routines to make going to bed as lazy as possible.

## How It Works

### Night Light Triggers Bedtime

When my night light turns on, everything in the living room turns off after 5 minutes. This includes all lights, media players, and TV. A "sleep well" message is also sent to my Home Assistant companion app.

### Activating Night Light

You can turn on the night light by:

- Clicking the bottom button on the living room lamp (Aqara switch) within a specific time frame
- Manually turning on the lamp via the companion app

### Phone Charging = Sleep Time

When I put my phone on the charger, the night light turns off - time to actually sleep. This also activates a helper so that if I unplug my phone during the night, the night light turns on again. I don't want this to happen when I unplug my phone during the day in the living room or at work, hence the helper. This helper resets to "off" at 10 AM.

### Spotify Sleep Timer

I often listen to a Spotify playlist before falling asleep but sometimes forget to set a sleep timer, so I created an automation for that too.

## Helper

```
input_boolean.bedtijd_automation_status
```

## Files

- [Bedtime - everything off](bedtime.yaml) - Turns off living room after night light is on for 5 minutes
- [Button trigger bedtime](button-trigger-bedtime.yaml) - Night light via Aqara button (22:00-06:00)
- [Sleep time](sleeptime.yaml) - Phone charging turns off night light and activates helper
- [Light on at night](light-on-at-night.yaml) - Night light on when unplugging phone at night
- [Reset automation](reset-automation.yaml) - Reset helper at 10 AM
- [Spotify off](spotify-off.yaml) - Pause Spotify after 30 minutes when going to bed