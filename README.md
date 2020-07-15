# nolevels
An Overhaul designed around removing effects of actor levels in Skyrim using the power of zEdit where possible.

# Design

## Actors

### Implementation:

- Given is a config file that contains races and values for their stats like health, ... as well as a deviation range.

A zEdit patcher goes through all race and NPC records in the loadorder and :
  a. Sets the stats in the race record to those set in the config
  b. Reads the old stats in each NPC record and actor race
  c. Gets the difference between the stat for the race and that set for the NPC based on the race
  d. Inputs that difference into a tanh function (ends up with a floating point value between -1 and 1)
  e. Multiplies the result with the deviation range set in the config
  f. Adds the result of that to the stat value from the race and sets it as the stat for the NPC
