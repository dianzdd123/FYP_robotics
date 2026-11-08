# GPT-Powered Multi-Robot Control

**MSEI Lab:** [Website](https://zhangrobotics.com/msei_website/) · [Website on GitHub](https://github.com/dianzdd123/msei_website)

## Start here

**Repository:** [dianzdd123/FYP_robotics](https://github.com/dianzdd123/FYP_robotics)

This repository is a fork of [Dan1678/FYP_robotics](https://github.com/Dan1678/FYP_robotics). Original authorship, citations and upstream notices are retained. Changes here apply to this fork.

**Scope:** Experimental hardware pipeline; robot endpoints, calibration, model weights and API access must be configured.

| Need | Where to start |
|---|---|
| Setup, file map, inputs/outputs and troubleshooting | [Reuse guide](docs/REUSE.md) |
| Local structural validation | `python scripts/check_repository.py` (Python 3.10+) |
| Proposed fixes and reproducibility details | [Contributing](CONTRIBUTING.md) |

The structural check does not run experiments or certify hardware, model accuracy or dependency compatibility. Reuse permissions need clarification: this checkout has no repository-wide licence file.


## Overview  
This repository implements a closed-loop multi-robot pick-and-place pipeline driven by large language models (LLMs) and vision networks. It combines:

- **Segmentation & Matching**  
  - **SAM2** for instance-agnostic mask generation  
  - **CLIP** for grounding masks to object names  
- **Task Planning**  
  - GPT-3.5/GPT-4 prompts to extract task objects, generate low-level motion commands, and decompose complex tasks  
- **Execution**  
  - TCP-based control scripts for one or two robots  
- **Verification & Retry**  
  - A second “verification” agent that confirms placements via vision and issues retries on failure  

## Entry points  
- Single-robot baseline (`SingleRobotSystem/single_robot_system.py`)
- Dual-robot (`DoubleRobotSystem/DualRobotSystem.py`)


## Dependencies

### Standard Library (built-in)
- `socket`
- `time`
- `json`
- `re`
- `pickle`

### Third-Party Packages
- `openai` == 0.28.1
- `opencv-python` (`cv2`) == 4.10.0.84
- `numpy` == 1.26.1
- `torch` == 2.5.0
- `Pillow` == 11.0.0
- `matplotlib` == 3.8.0

### External Repositories (SAM2 should be cloned into project root)
- `clip` – (https://github.com/openai/CLIP)
- `SAM2` – (https://github.com/facebookresearch/sam2)
