# 🏠 Presence Detection System

Reliable dual-tracker system for accurate home/away detection using GPS and WiFi connectivity.

---

## 📋 Problem Statement

### The Challenge

Standard GPS-based presence detection often fails due to:

- **Delayed updates** from phone sensors
- **GPS accuracy issues** in urban environments  
- **Battery optimization** blocking location updates
- **Automation failures** due to unreliable triggers

### The Solution

Implement a **dual device tracker system** that combines:

1. **GPS location tracking** for broader area detection
2. **WiFi connection monitoring** for immediate home detection

---

## 🏗️ Architecture Overview

### Two-Tracker Approach

#### 1. GPS Device Tracker

- **Purpose**: Broad area presence (home, work, neighborhood)
- **Reliability**: Medium (subject to GPS delays)
- **Setup**: Built-in Home Assistant zones

#### 2. WiFi Device Tracker  

- **Purpose**: Immediate home detection
- **Reliability**: High (instant connection detection)
- **Setup**: Custom MQTT-based solution

### Why This Works

- **Redundancy**: Two independent detection methods
- **Speed**: WiFi provides instant home detection
- **Flexibility**: GPS provides location context beyond home
- **Reliability**: System works even if one tracker fails

---

## 📱 Android Companion App Setup

### Required Sensors

Enable these sensors in the Home Assistant Companion App:

- ✅ **WiFi Connection** sensor
- ✅ **GPS Location** sensor

### Location Permissions

- Grant **precise location** access
- Disable **battery optimization** for HA app
- Enable **background app refresh**

---

## 🗺️ GPS Zone Configuration

### Zone Setup in Home Assistant

1. **Navigate**: `Settings` → `Areas & Zones` → `Zones`
2. **Create zones**:
   - `Home` (your house location)
   - `Work` (optional - work location) 
   - `Neighborhood` (broader area around home)

### Person Assignment

1. **Navigate**: `Settings` → `People`
2. **Select person** to configure
3. **Add device** under "Select the devices that belong to this person"
4. **Choose** your phone's GPS tracker

---

## 📶 WiFi-Based Detection

### MQTT Integration Required

This method requires MQTT broker setup. [📖 Installation guide](https://www.home-assistant.io/integrations/mqtt)

### Configuration Steps

1. **Add to `configuration.yaml`**:

   ```yaml
   mqtt: !include mqtt.yaml
   ```

2. **Create `mqtt.yaml`** with device tracker config

3. **Import WiFi automation** for connection monitoring

### Smart Delay Logic

- **Connection detected**: Immediate `home` status
- **Connection lost**: 30-second delay before `not_home`
- **Why delay?**: Prevents false triggers when stepping outside briefly

---

### Core Configuration

| File | Purpose |
|------|---------|
| [`mqtt.yaml`](mqtt.yaml) | MQTT device tracker setup |
| [`wifi_connection.yaml`](wifi_connection.yaml) | WiFi monitoring automation |

