# Vacuum Robot

I want my robot vacuum to clean only when I am not at home. It should sweep at 10:00 AM and mop at 3:00 PM. However, if it did not sweep at 10:00 AM and I am not home at 3:00 PM, it should still sweep at 3:00 PM.

## Design Choices

**Why presence-based cleaning?**

- Avoids disturbing me while working from home
- Only cleans when space is unoccupied

**Why intelligent scheduling?**

- Maintains daily cleaning routine even if morning schedule is missed
- Prioritizes sweeping over mopping for better results

## Presence Detection

I use two device trackers to check if I am home, or around the neighbourhood or not at home at all. [More info](../home_or_away/README.md)

## Helper

That's why I created a helper to keep track of whether the robot has done its round at 10:00 AM. This helper is reset every night.

`input_boolean.cleaned_at_10_am_today`

## Automations

I have created three automations for this:

- [`reset_helper`](reset_helper.yaml) - Resets the tracker at midnight
- [`when_time_is_10`](10hour.yaml) - Morning cleaning (sweeping)
- [`when_time_is_15`](15hour.yaml) - Afternoon cleaning (mopping or sweeping)

## Logic

### 10:00 AM

If not home: sweep and mark helper as "on"

### 3:00 PM  

If not home:

- If helper is "on": mop (already swept today)
- If helper is "off": sweep (missed morning cleaning)

### Midnight

Reset helper to "off" for the next day

### Yaml files

- [`reset_helper.yaml`](reset_helper.yaml) - Daily state reset
- [`10hour.yaml`](10hour.yaml) - Morning cleaning routine
- [`15hour.yaml`](15hour.yaml) - Afternoon cleaning logic
