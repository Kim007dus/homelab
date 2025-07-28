# 🏠 Home Assistant Automations

Welcome to the Home Assistant section of my homelab!  
Here you'll find all my automations, helpers, and integrations for a smarter, safer, and more comfortable home.

---

## 📚 Contents

- [Purpose & Learning Goals](#purpose--learning-goals)
- [Structure](#structure)
- [Automations](#automations)
  - [Vacuum Robot](./Vacuum%20Robot/)
  - [Lights](./Lights/) *(in progress)*
  - [Living Room](./Woonkamer/) *(in progress)*
- [How to Use?](#how-to-use)
- [Contributing](#contributing)
- [License](#license)

---

## Purpose & Learning Goals

**Why this directory?**
- To automate and make my home smarter with Home Assistant.
- To learn YAML, automation logic, and integrations.
- To apply best practices for scalable, reusable automations.
- To connect with other homelab components (like Ansible, monitoring, PKI).

**Learning goals:**
- Set up more complex automations with conditional logic.
- Use helpers (`input_boolean`, `input_datetime`, etc.) for status and state management.
- Integrate different devices and platforms.
- Document and share automations for personal use and the community.

---

## Structure

This directory is organized by type of automation or room.  
Each subfolder contains its own README with explanations, choices, and examples.

```
home_assistant/
│
├── README.md                # This file (overview & explanation)
├── Vacuum Robot/            # Automations for the robot vacuum
│   └── README.md
├── Lights/                  # Automations for lighting (in progress)
│   └── README.md
└── Woonkamer/               # Automations for the living room (in progress)
    └── README.md
```

---

## Automations

### [Vacuum Robot](./Vacuum%20Robot/)

Automations for smart control of my robot vacuum, depending on presence and time.  
See the [README in the Vacuum Robot folder](./Vacuum%20Robot/README.md) for details.

### [Lights](./Lights/) *(in progress)*

Automations for smart lighting will be added here.

---

## How to Use?

1. Copy the YAML files from the desired folder to your own Home Assistant `automations` folder.
2. Create the required helpers via the UI or YAML.
3. Adjust entity_ids to match your devices.
4. Import the automations via the Home Assistant UI or YAML configuration.

---

## Contributing

Improvements, extensions, or suggestions are welcome via pull request or issue!

---

## License

MIT License - see [LICENSE](LICENSE) for details.

---

> Part of my [🏠 Homelab project](../README.md).
