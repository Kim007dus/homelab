# Energy Dashboard

I chose to start reading my smart meter because I have a dynamic energy/gas contract since September. This allows me to align my energy consumption with current prices and potentially save money.

## Hardware

### Smart Meter Reader

I use this dongle: https://www.hashop.nl/wifi-P1-Pro-voor-Home-Assistant

### Energy Monitoring

Currently I have 1 Matter smart plug from Eve that also monitors energy consumption. Unfortunately, the TP-Link plug doesn't do this yet because it hasn't been updated to the latest version of Matter. I do have one at home and can monitor another device's power consumption as soon as this update is released.

## Goal

**Why energy monitoring?**

- Dynamic energy contract allows price-based consumption optimization
- Real-time monitoring helps identify energy-hungry devices
- Potential cost savings by shifting usage to cheaper hours

## Washing Machine Power Control

I noticed in the dashboard that my washing machine consumes power even when it's not running. Since I have a smart plug on it, I thought I could do something with that, but I don't want to grab my phone every time to turn on the power when I start the washing machine. Then I remembered I have a door sensor on my washing machine, so I created an automation for that.

**Logic:**

- Door closes: Turn on washing machine power
- Door opens (for 1 minute): Turn off washing machine power

**Files:**

- [Power off](washingmachine-off.yaml)
- [Power on](washingmachine-on.yaml)