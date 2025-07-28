# Vacuum Robot

I want my robot vacuum to clean only when I am not at home. It should sweep at 10:00 AM and mop at 3:00 PM. However, if it did not sweep at 10:00 AM and I am not home at 3:00 PM, it should still sweep at 3:00 PM.

I use two device trackers to check if I am home or not. [More info](/homelab/homelab/home_assistant/Home%20or%20Away/)

That’s why I created a helper to keep track of whether the robot has done its round at 10:00 AM. This helper is reset every night.

`input_boolean.cleaned_at_10_am_today`

I have created three automations for this:

- [`reset_helper`](reset_helper.yaml)
- [`when_time_is_10`](10hour.yaml)
- [`when_time_is_15`](15hour.yaml)