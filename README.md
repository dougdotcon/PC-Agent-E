# PC Agent-E

<p align="center">
  📄 <a href="https://arxiv.org/abs/2505.13909" target="_blank">Paper</a> &nbsp; | &nbsp;
  🌐 <a href="https://gair-nlp.github.io/PC-Agent-E" target="_blank">Website</a> &nbsp; | &nbsp;
  🤖 <a href="https://huggingface.co/henryhe0123/PC-Agent-E" target="_blank">Model</a> &nbsp; | &nbsp;
  🤗 <a href="https://huggingface.co/datasets/henryhe0123/PC-Agent-E" target="_blank">Dataset</a>
</p>

<p align="center">
  <img src="./assets/first_image.png" width="50%" alt="PC Agent-E Animation">
</p>

## Overview

PC Agent-E is an efficient agent training framework for computer use that elicits strong capabilities with remarkable data efficiency. The implementation consists of four key components:

1. **Trajectory Collection**: Gather task trajectories from human annotators using [PC Tracker](https://github.com/GAIR-NLP/PC-Agent?tab=readme-ov-file#pc-tracker)
2. **Thought Completion**: Reconstruct the latent human thought process preceding each action
3. **Trajectory Boost**: Synthesize diverse alternative action decisions
4. **Agent Training**: Train the native agent model using augmented trajectories

![Framework Overview](./assets/overview.png)

## Key Results

Performance on WindowsAgentArena-V2 benchmark (Success Rate %):

| Model | LibreOffice | Chrome | Edge | System | VS Code | VLC | Utils | Total |
|-------|-------------|--------|------|--------|---------|-----|-------|-------|
| Qwen2.5-VL-72B | 0.0 | 34.7 | 15.4 | 20.8 | 26.3 | 7.6 | 16.7 | 14.9 |
| UI-TARS-1.5-7B | **7.1** | 34.7 | 23.1 | 45.8 | 21.1 | 7.6 | 16.7 | 21.3 |
| UI-TARS-72B-DPO | 0.0 | 40.6 | 38.5 | 58.3 | 36.8 | 7.6 | 25.0 | 26.2 |
| Claude 3.7 Sonnet | 2.4 | 46.5 | **61.5** | 54.2 | 52.6 | 29.0 | 16.7 | 32.6 |
| Claude 3.7 Sonnet (thinking) | 2.4 | **64.1** | 46.2 | **66.7** | 52.6 | 21.9 | 25.0 | 35.4 |
| **PC Agent-E (Ours)** | 4.8 | **64.1** | 46.2 | 50.0 | **57.9** | **35.7** | **33.3** | **36.0** |

## Demo

Watch PC Agent-E autonomously controlling a computer to complete tasks on Windows and Linux systems.

[![Demo Video 1](https://github.com/user-attachments/assets/9540d8cb-630d-41e2-a108-a96ca3fcb32e)](https://github.com/user-attachments/assets/9540d8cb-630d-41e2-a108-a96ca3fcb32e)

[![Demo Video 2](https://github.com/user-attachments/assets/18b436e7-733f-49a5-8716-25c29a990766)](https://github.com/user-attachments/assets/18b436e7-733f-49a5-8716-25c29a990766)

## Quick Start

### 1. Trajectory Collection

Collect raw human trajectory using PC Tracker. Refer to the [PC Tracker documentation](https://github.com/GAIR-NLP/PC-Agent?tab=readme-ov-file#pc-tracker) for usage instructions.

### 2. Post Processing

Convert raw trajectories into high-quality training data:

1. Place recorded data in the `data/` directory
2. Execute the post-processing pipeline:
   bash
   python scripts/postprocess.py --input data/raw --output data/processed
   

### 3. Thought Completion

Reconstruct human reasoning behind actions:

bash
python scripts/thought_completion.py --data data/processed


### 4. Trajectory Boosting

Generate diverse action alternatives:

bash
python scripts/trajectory_boost.py --data data/processed --boost-factor 3


### 5. Model Training

Train the agent with augmented trajectories:

bash
python train.py --config configs/pc_agent_e.yaml --data data/augmented


## Installation

### Prerequisites

- Python 3.10+
- PyTorch 2.0+
- CUDA 11.8+ (if using GPU)

### Setup

bash
# Clone the repository
git clone https://github.com/GAIR-NLP/PC-Agent-E.git
cd PC-Agent-E

# Create virtual environment
python -m venv pc_agent_env
source pc_agent_env/bin/activate  # Linux/Mac
# pc_agent_env\Scripts\activate  # Windows

# Install dependencies
pip install -r requirements.txt


## Architecture

The framework follows a systematic pipeline:

1. **Data Collection Layer**: Captures human-computer interactions via PC Tracker
2. **Processing Layer**: Enriches trajectories with thought completion and boosting
3. **Training Layer**: Supervises model on augmented dataset
4. **Inference Layer**: Executes actions in real-world environments

## Citation

bibtex
@article{he2025pcagent_e,
  title={Efficient Agent Training for Computer Use},
  author={He, Henry and others},
  journal={arXiv preprint arXiv:2505.13909},
  year={2025}
}


## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

Contributions are welcome! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting a pull request.

## Questions?

For technical questions, please open an issue on GitHub. For research inquiries, contact the authors via the paper.