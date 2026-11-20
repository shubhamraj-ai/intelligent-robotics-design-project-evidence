# Intelligent Robotics Design Project Evidence

**University of Aberdeen - EG505P / EG506P: Intelligent Robotics for Energy Infrastructure**

This repository is a compact, assessment-facing technical evidence archive for a CoppeliaSim design project on camera-based autonomous maze navigation and ultrasonic maze mapping.

It intentionally contains only the final technical deliverables and the validation evidence needed to understand the project development route. Course-provided scene files, large diagnostic datasets, caches, virtual environments and unrelated historical branches are deliberately excluded.

## Final system

The final navigation pipeline is intentionally simple:

`50 x 50 camera image -> grayscale/normalisation -> 2500-input, 3-output softmax perceptron -> lightweight supervisory checks -> wheel commands`

The neural network remains the primary navigator. In the representative clean V2 acceptance run, **483 of 486 movement pulses (99.38%)** used the raw neural-network action directly. Only three pulses were corrected by the lightweight supervisor at visually ambiguous right-turn entrances.

This value is **prediction-to-applied-action agreement during live navigation**, not held-out classification accuracy.

## Repository structure

### final-deliverables/
The seven frozen technical deliverables prepared for submission:

- dataset.zip
- training.ipynb
- network.h5
- robotcontrol.py
- navigation.py
- sensordata.txt
- mazemapping.m

### validation-baselines/
Preserved engineering checkpoints used during iterative development:

- **Golden** - first preserved successful full autonomous traversal and terminal stop.
- **Diamond** - preserved navigation baseline extended to Step-7 ultrasonic acquisition and mapping.
- **Platinum** - simplified controller that completed the route but exposed a turn-state bookkeeping issue.
- **Platinum V2** - corrected simplified baseline that recognised the naturally NN-executed fourth right turn and completed the maze with clean terminal stopping.

These names are validation checkpoints, not separate algorithms.

### evidence/
Compact supporting artefacts for autonomous-navigation validation, manual robot-control stability, ultrasonic maze reconstruction, and SHA-256 validation of the final technical package.

## Representative validation result

| Measure | Representative V2 run |
|---|---:|
| Total movement pulses | 486 |
| NN action applied directly | 483 |
| Supervisory overrides | 3 |
| Direct NN/action agreement | 99.38% |
| Outcome | Full maze + terminal stop |

A second successful V2 run recorded 482 direct NN actions from 488 movement pulses (98.77%). Across the two successful V2 runs, 965 of 974 pulses (99.08%) followed the raw NN action directly.

## Training and mapping notes

- Final labelled dataset: **426 images**
- Class distribution: **338 forward, 52 left, 36 right**
- Camera/training resolution: **50 x 50 pixels**
- Model: **single Dense/softmax perceptron-style classifier; no CNN**
- Final sensor dataset: **499 pose/range samples**
- Mapping: MATLAB geometric projection of valid front/left/right/rear sensor measurements into world coordinates

## Scope and provenance

The original maze scene supplied through the course is **not redistributed in this public repository**. This archive contains student-created technical deliverables and selected validation evidence only.

The full development-history repository is separate. This evidence repository is intentionally kept simple so that a marker or reviewer can inspect the final work and the Golden/Diamond/Platinum/V2 development route without navigating diagnostic branches.

## Citation

A CITATION.cff file and REPORT_CITATION.md are provided. For the project report, cite the stable report-evidence-v1.0 tag rather than the moving main branch.