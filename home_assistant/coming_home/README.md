# Coming Home or Going Away

When I leave home, I want everything to turn off automatically to save energy and so I can't forget to leave lights on all day. When I come home, I like a playlist to start playing and some more light in the living room to make it more cozy.

I use two device trackers to check if I am home, or around the neighbourhood or not at home at all. [More info](../home_or_away/README.md)

## Coming Home

When I come home the following happens:
As soon as I'm in the neighborhood or just arrived home and the door opens, a lamp turns on in the living room and my playlist starts playing. If the washing machine has finished, the WC light also turns red, so I know I need to take the laundry out of the washing machine.

**Conditions:**

- Door opens AND (in neighborhood zone OR person state is "Heading home")

**Daytime (10:00-20:00):**

- Turn on corridor light
- Start Spotify playlist at low volume
- Wake up media player

**Nighttime (20:00-10:00):**

- Only corridor light (no music)

**Laundry alert:**

- WC light turns red if washing machine finished

## Going Away

When I leave home and am away for more than 2 minutes, all lights and media players turn off.

**Actions:**

- Turn off all media players
- Stop any playing media  
- Turn off non-essential lights

## Yaml Files

- [Coming home](cominghome.yaml)
- [Going away](goingaway.yaml)