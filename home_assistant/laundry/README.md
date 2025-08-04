# Laundry Automation

I'm quite chaotic and often forget that my washing machine has finished, so I wanted to get a notification as soon as my 'dumb' washing machine is done. For this I bought an Eve plug with energy monitoring and a door sensor for my washing machine door.

## Design Choice

**Why energy monitoring + door sensor?**

- Energy monitoring detects when machine stops running
- Door sensor confirms when laundry is removed
- Combines both signals for accurate status tracking

## Helper

I use a helper to track the washing machine status:

```
input_select.wasmachine_status
```

With the statuses:

- `running` - Machine is currently washing
- `done` - Washing finished, laundry needs to be removed  
- `off` - Machine is off or laundry has been removed

## How it Works

By combining energy monitoring with the status helper, I can turn on lights and send notifications as soon as the washing machine is finished.

## Files

- [Done](laundry-done.yaml) - When washing cycle completes
- [Running](laundry-running.yaml) - When machine starts washing
- [Off](laundry-off.yaml) - When machine is turned off or door opened