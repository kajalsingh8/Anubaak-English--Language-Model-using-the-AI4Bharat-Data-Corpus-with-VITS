

Anubaak: Non-Hindi Speech Synthesis Model using VITS and AI4Bharat Corpus

## Project Overview
This project involves training a speech synthesis model using the VITS (Variational Inference Text-to-Speech) architecture on a non-Hindi language selected from the AI4Bharat data corpus. The model aims to generate high-quality audio from text inputs and is configured to stream WAV audio as FLAC audio using a WebSocket connection.

## Objective
- Develop a robust TTS (Text-to-Speech) model for a lesser-represented language within the AI4Bharat corpus.
- Ensure audio-to-text streaming functionality with WebSocket support for FLAC conversion.
- Avoid the use of news datasets.

---

## Table of Contents
1. [Project Setup](#project-setup)
2. [Data Preparation](#data-preparation)
3. [Model Configuration and Training](#model-configuration-and-training)
4. [Model Evaluation](#model-evaluation)
5. [Deployment](#deployment)
6. [Usage Instructions](#usage-instructions)
7. [Optimization](#optimization)
8. [Project Documentation](#project-documentation)
9. [License](#license)

---

## Project Setup

### Prerequisites
- Google Colab or a machine with a compatible GPU setup
- Python 3.7+
- Git
- Docker (optional, for advanced deployment)
- WebSocket libraries for audio streaming

### Installation
1. Clone the VITS repository and this project:
    ```bash
    git clone https://github.com/jaywalnut310/vits.git
    cd vits
    ```

2. Install dependencies:
    ```bash
    pip install -r requirements.txt
    ```

3. Set up additional dependencies for AI4Bharat data handling:
    ```bash
    pip install torchaudio librosa websocket
    ```

4. Download and configure the AI4Bharat dataset:
   - Follow data usage rights and guidelines provided by [AI4Bharat Indic Voices](https://indic-tts-data.ai4bharat.org/) and [Svarah](https://github.com/AI4Bharat/indic-synthesis).

5. Configure your language-specific dataset path within the `config.json` file.

## Data Preparation

1. **Dataset Download**: Download the selected dataset from AI4Bharat Indic Voices (or Svarah), focusing on non-news sources.
2. **Pre-processing**:
    - Normalize audio samples to ensure consistency in volume and clarity.
    - Clean transcripts and match them with audio files.
3. **Data Splitting**:
    - Split the dataset into training, validation, and test sets (80/10/10).

## Model Configuration and Training

1. **Configuration**: Adjust the `config.json` file to accommodate the specifics of the selected language and dataset.
   - Define data paths, sample rates, and other dataset-specific parameters.
   
2. **Training**: Run the training script, specifying the training data and necessary hyperparameters:
    ```python
    python train.py --config_path config.json
    ```
3. **Monitoring**: Keep track of accuracy and loss metrics. Tuning learning rates or batch sizes may help to achieve better results.

## Model Evaluation

After training, evaluate the model using validation and test datasets to measure synthesis quality.

```python
python evaluate.py --config_path config.json --model_path path/to/model_checkpoint
```

Expected outputs:
- **Validation Loss**: Measures model performance on unseen data.
- **Generated Audio**: Sample WAV files for subjective quality checks.

## Deployment

1. **WebSocket Integration**:
   - To allow real-time WAV to FLAC conversion, set up a WebSocket server:
   ```python
   python websocket_server.py --port 6789
   ```
2. **Audio Conversion**: Stream synthesized audio through the WebSocket for real-time format conversion.

## Usage Instructions

1. **Start the WebSocket Server**:
    ```bash
    python websocket_server.py
    ```

2. **Run Inference**:
    ```python
    python infer.py --text "Your text here" --model_path path/to/model_checkpoint
    ```
   
3. **Connect to WebSocket**: Users can connect to the server to receive FLAC audio outputs.

## Optimization

To improve model performance:
- Fine-tune hyperparameters, including learning rate and batch size.
- Experiment with data augmentation techniques, such as noise addition or pitch alteration.

## Project Documentation

All code and configurations are stored in a private GitHub repository. For access, please contact **tech@peritys.com** to request collaborator access.

The repository includes:
- **Training scripts**: Code to process and train the model on non-Hindi language datasets.
- **WebSocket server**: For real-time WAV to FLAC audio streaming.
- **Evaluation and testing scripts**: Tools for assessing model performance.

