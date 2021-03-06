# nolevels
An Overhaul designed around removing effects of actor levels in Skyrim using the power of zEdit where possible.

# Design

## Actors

### Exposed Settings to User

For each Race:
```
Health                    // Main Health
Health Regen              // How fast Health should regen
Health Deviation_range    // The range Health offsets can be in
Magicka
Magicka Regen
Magicka Deviation_range
Stamina
Stamina Regen
Stamina Deviation Range
Carryweight               // Base Carryweight for the race
```

Global Settings for the Patcher:
```
  Patch Race Health
  Patch Race Health Regen
  Patch Race Magicka
  Patch Race Magicka Regen
  Patch Race Stamina
  Patch Race Stamina Regen
  Patch Carrweight
  Patch all NPCs to be level 1
  
  Patch Health Offsets, Remove them or leave them alone
  Patch Magicka Offsets, Remove them or leave them alone
  Patch Stamina Offsets, Remove them or leave them alone
  
  Combat Health Regen Rate Mult
  Combat Magicka Regen Rate Mult
  Combat Stamina Regen Rate Mult
```

### Implementation

- Given is a config file that contains races and values for their stats like health, ... as well as a deviation range.

The patcher goes through all RACE records:

  1. Sets the stats in the race record to those set in the config
 
The patcher goes through all NPC_ records:
  
  2. Reads the old stat offsets in each NPC_ record
  
  3. If the stat offset is not 0 (for each stat)
      
    1. Input the offset into the `Math.tanh` function (ends up with a floating point value between -1 and 1)
  
    2. Multiplies the result with the deviation range set in the config
  
    3. Set the result as new stat Offset

The Patcher changes / adds settings:

`fNPCHealthLevelBonus` is set to 0.

`fCombatHealthRegenRateMult` is set to value in config.

`fCombatMagickaRegenRateMult` is set to value in config.

`fCombatStaminaRegenRateMult` is set to value in config.
