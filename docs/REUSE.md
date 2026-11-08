# Reusing FYP_robotics

Language-guided single- and dual-robot manipulation.

**Current scope:** Experimental hardware pipeline; robot endpoints, calibration, model weights and API access must be configured.

This repository is a fork of [Dan1678/FYP_robotics](https://github.com/Dan1678/FYP_robotics). Original authorship, citations and upstream notices are retained. Changes here apply to this fork.

## Setup

Create an isolated Python environment. The README records the original package versions, including the legacy `openai==0.28.1` interface. SAM2 and CLIP come from their respective source repositories; their compatibility with the selected PyTorch build must be checked before hardware use. The repository does not include a locked, end-to-end environment or model weights.

```bash
python scripts/check_repository.py
```

## Actual entry points

| Path | Purpose |
|---|---|
| `SingleRobotSystem/single_robot_system.py` | Single-robot orchestration |
| `DoubleRobotSystem/DualRobotSystem.py` | Dual-robot orchestration; note the exact capitalisation |
| `Perception/segmentation_layer.py` | Segmentation and image matching |
| `Perception/clip_layer.py` | CLIP matching support |
| `Planning/gpt_functions.py` | Language-model planning requests |
| `Execution/client_script.py` | TCP command transport |
| `Mapping/Calibration/Json/` | Example calibration files |
| `Testing/` | Camera, planning and physical-system diagnostics |

Run from the repository root using module syntax so sibling packages can be imported: `python -m SingleRobotSystem.single_robot_system` or `python -m DoubleRobotSystem.DualRobotSystem`. These are hardware entry points, not smoke tests. Configure them before execution.

## Required local inputs

1. Set the robot IP addresses and integer TCP ports in the chosen entry point.
2. Supply the SAM2 configuration and checkpoint expected by the perception code.
3. Recalibrate image-to-robot mappings and bin/gripper poses for your camera and robot. Included numbers are examples from the original setup.
4. Review every `open(...)` and model path: some code expects calibration JSON in the working directory although examples are stored under `Mapping/Calibration/Json/`.
5. Configure authorised API credentials locally; do not commit credentials or use public issues for private data.

The system produces segmentation/matching results and sends motion commands. Files in `Testing/` may access cameras, external services or robot hardware. They are not an unattended unit-test suite. Start with recorded-image perception and inspect proposed commands before connecting a calibrated robot.

## Troubleshooting

A missing `Perception` or `Mapping` import usually indicates the wrong working directory or direct execution of a nested script. Missing calibration JSON means the configured path does not match its actual location. Connection failures require checking both the robot-side listener and client endpoint; changing the perception model will not fix transport failures.

## Attribution and reuse permissions

No repository-wide licence file is included in this checkout. Confirm reuse and redistribution permissions with the relevant rights holders; this maintenance update does not add a licence or relicense upstream code, data or assets.

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for the local workflow and what to include with a proposed change.
