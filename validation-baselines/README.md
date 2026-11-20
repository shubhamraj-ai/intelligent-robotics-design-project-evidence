# Validation Baselines

The baseline names are project-defined engineering checkpoints used to preserve stable controller states during iterative testing.

## Golden

The Golden checkpoint represents the first preserved successful full autonomous-navigation gate. The compact log records four right-turn events and terminal-wall stopping.

## Diamond

Diamond preserved the validated navigation controller while extending the project to Step-7 ultrasonic data acquisition and offline mapping. The folder includes the navigation/model baseline, compact live-navigation evidence and sensor-geometry evidence.

## Platinum

Platinum simplified the supervisory architecture and completed the route, but testing showed that internal turn-state bookkeeping could remain one turn behind after a right turn that the neural network had already completed naturally.

## Platinum V2

Platinum V2 corrected that state interpretation rather than forcing another route command. In the representative acceptance run:

- 486 movement pulses were executed;
- 483 neural-network predictions were applied directly;
- 3 pulses were corrected by the supervisor;
- direct NN/action agreement was 99.38%;
- the robot completed the maze and stopped at the terminal wall.

The checkpoints document iterative engineering and evidence preservation; they are not separate navigation algorithms.