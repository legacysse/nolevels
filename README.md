# nolevels
An Overhaul designed around removing effects of actor levels in Skyrim using the power of zEdit where possible.

# Design

## Actors

### Implementation:

- Given is a config file that contains races and values for their stats like health, ... as well as a deviation range.

A zEdit patcher goes through all race and NPC records in the loadorder and :

  1. Sets the stats in the race record to those set in the config
  
  2. Reads the old stat offsets in each NPC record and actor race
  
  3. If the stat offset is not 0 (for each stat)
      
    1. Input the offset into the `Math.tanh` function (ends up with a floating point value between -1 and 1)
  
    2. Multiplies the result with the deviation range set in the config
  
    3. Set the result as new stat Offset
