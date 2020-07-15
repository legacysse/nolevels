# nolevels
An Overhaul designed around removing effects of actor levels in Skyrim using the power of zEdit where possible.

# Design

## Actors

### Implementation:

- Given is a config file that contains races and values for their stats like health, ... as well as a deviation range.

A zEdit patcher goes through all race and NPC records in the loadorder and :

  1. Sets the stats in the race record to those set in the config
  
  2. Reads the old stats in each NPC record and actor race
  
  3. Gets the difference between the stat for the race and that set for the NPC based on the race
  
  4. Inputs that difference into a tanh function (ends up with a floating point value between -1 and 1)
  
  5. Multiplies the result with the deviation range set in the config
  
  6. Adds the result of that to the stat value from the race and sets it as the stat for the NPC
