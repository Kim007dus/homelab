# Lights

I have a lot of routines and I wanted to automate my lights to make my home smarter. I started by buying an Aqara smart switch for my corridor. Now I have various lights from smart plugs, smart switches, and smart bulbs.

I use two device trackers to check if I am home, or around the neighbourhood or not at home at all. [More info](../home_or_away/README.md)

## Goal

The goal is to never have to manually turn lights on or off anymore - maximum laziness! This includes the following automations:

## Sunset Lighting

Lights in the living room turn on 45 minutes before sunset. If I'm not home, only a table lamp turns on. When I'm away, all lights automatically turn off at 1:00 AM.

**Files:**

- [Sunset](sunset.yaml)
- [Not home lights off](not-home-lights-off.yaml)

## Corridor Light

When the front door opens, the corridor light always turns on. It automatically turns off after 10 minutes, even if manually controlled. For this I created a helper and two automations to manage this helper.

**Helper:**

```
input_boolean.ganglicht_aan
```

**Files:**

- [Helper on](helper-on.yaml)
- [Helper off](helper-off.yaml)  
- [Door open light on](door-open-light-on.yaml)
- [Corridor lights off](corridor-lights-off.yaml)

## Motion Detection - WC

I have a motion sensor in my WC that turns on the light when someone enters. The light turns off after 2 minutes when no motion is detected.

**Files:**

- [Toilet](wc.yaml)

## Design Choices

**Why helper for corridor light?**

- Tracks light state independently of physical switch
- Ensures 10-minute auto-off works even after manual control
- Prevents timing conflicts between automations

**Why different behavior when away?**

- Security simulation with table lamp
- Energy saving by turning off non-essential lights
- Maintains some activity appearance from outside