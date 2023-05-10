# MSCS-271-ForestFireDynamics

# Authors: Caleb Czeck and Lucas Schaff

## User Input Variables

- `plantGrowthState0To1` - the percentage chance of a patch in `plantGrowthState = 0` transitioning to `plantGrowthState = 1` when it has a neighbor with `plantGrowthState = 4`.
 
- `plantGrowthState1To2` - the percentage chance of a patch in `plantGrowthState = 1` transitioning to `plantGrowthState = 2`.

- `plantGrowthState2To3` - the percentage chance of a patch in `plantGrowthState = 2` transitioning to `plantGrowthState = 3`.

- `plantGrowthState3To4` - the percentage chance of a patch in `plantGrowthState = 3` transitioning to `plantGrowthState = 4`.

-`minPlantLife` - the minimum life of a `plant` as defined by a patch with `plantGrowthState != 0`.

-`maxPlantLife` - the maximum life of a `plant` as defined by a patch with `plantGrowthState != 0`.

-`seedBurnChance` - the percentage chance of a patch with `plantGrowthState = 1` to transition to `fireState = 2` when a neighbor is in `fireState = 1` or `fireState = 2`.

-`fireState1SpreadChance` - the percentage chance of a patch with `fireState = 0` transitioning to `fireState = 1` when a neighbor is in `fireState = 1`.

-`fireState2SpreadChacne` - the percentage chance of a patch with `fireState = 0` tranistioning to `fireState = 1` when a neighbor is in `fireState = 2`.

-`fireState1To2` - the percentage chance of a patch with `fireState = 1` transitioning to `fireState = 2`.

-`ashClearChance` - the percentage chance of a patch with `fireState = 3` transitioning to `fireState = 0` and `plantState = 0`.

-`control-type` - the shape of the controlled area.

## Code Global Variables

- `plantColors` - a list of patch colors corresponding to plant growth states.

- `fireColors` - a list of patch colors corresponding to fire states.

## Procedures

- `setup` - setup the simulation.

- `go` - run the `trasition-plants` and `transition-fire` procedures.

- `transition-plants` - transitions between plant states.
  - `plantGrowthState = -1` - The `plantGrowthState` remains `-1`.
  - `plantGrowthState = 0` - The patch checks its cardinal neighbors. If at least one has `plantGrowthState = 4`, then the patch has a chance to transition to `plantGrowthState 1`.
  - `plantGrowthState = 1` - The patch has a chance to transition to `plantGrowthState 1`.
  - `plantGrowthState = 2` - If the patch's cardinal neighbors all have `plantGrowthState = 4`, then the patch's `plantGrowthState = 0`. In other words, the plant dies. Otherwise, the patch has a chance to transition to `plantGrowthState 3`.
  - `plantGrowthState = 3` - The patch has a chance to transition to `plantGrowthState = 4`.
  - `plantGrowthState = 4` - The patch remains at `plantGrowthState = 4`.

  - At any time, a patch will transition to `plantGrowthState = 0` if `plantDeathTimer = 0`.

- `transition-fire` - transitions between fire states.
  - `fireState = -1` - The `fireState` remains `-1`.
  - `fireState = 0` - The patch is flammable if `plantGrowthState != 0`. If it is flammable and one of its cardinal neighbors has `fireState = 1`, then the patch has a chance to transition to `fireState = 1` and `plantGrowthState = -1`. Ig `plantGrowthState = 1`, then the patch has a chance to catch fire and move to `fireState = 2`.
  - `fireState = 1` - The patch has a chance to transition to `fireState = 2`.
  - `fireState = 2` - If the fire has reached the end of its life, the patch has a chance to transition to `fireState = 3`.
  - `fireState = 3` - The patch has a chance to transition to `fireState = 0` and `plantGrowthState = 0`.

- `startFire` - Starts a fire on a random patch with `plantState` of `2`, `3`, or `4`.