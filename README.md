# Sentiment Analysis

This repository contains a complete pipeline for Sentiment Analysis, including data versioning, model training, evaluation, and deployment. It uses DVC for data and experiment management, a Flask-based REST API for serving models, and Docker/Kubernetes for containerized deployment.

## Table of Contents

* [Features](#features)
* [Repository Structure](#repository-structure)
* [Installation](#installation)
* [Data Management with DVC](#data-management-with-dvc)
* [Training and Evaluation](#training-and-evaluation)
* [API Service](#api-service)
* [Deployment](#deployment)
* [Testing](#testing)
* [Dependencies](#dependencies)
* [Contributing](#contributing)
* [License](#license)

## Features

* **Data Versioning**: Track datasets, preprocessing steps, and model artifacts using DVC.
* **Modular Codebase**: Clear separation of concerns with folders for data processing, model training, and inference.
* **Experiment Tracking**: Reproducible experiments via DVC and `params.yaml`.
* **REST API**: Flask app (`flask_app/`) to serve the trained model for inference.
* **Containerization**: Dockerfile for building consistent environments.
* **Kubernetes Deployment**: `deployment.yaml` for easy cluster deployment.
* **Automated Testing**: Unit and integration tests in `tests/` with `tox` configuration.

## Repository Structure

```
├── .github/           # GitHub Actions CI workflows
├── .dvc/              # DVC metadata
├── flask_app/         # Flask API code for inference
├── models/            # Trained model artifacts
├── notebooks/         # Exploratory and analysis notebooks
├── reports/           # Generated reports and visualizations
├── scripts/           # Utility scripts (data download, preprocessing)
├── src/               # Core NLP modules and training scripts
├── tests/             # Unit and integration tests
├── .gitignore
├── .dvcignore
├── deployment.yaml    # Kubernetes deployment manifest
├── Dockerfile         # Docker image specification
├── Makefile           # Common commands: `make train`, `make run-api`, etc.
├── params.yaml        # Hyperparameters and settings
├── requirements.txt   # Python dependencies
├── setup.py           # Package installation script
├── test_environment.py# Environment validation script
├── tox.ini            # Testing environment configuration
└── README.md          # This file
```

## Installation

1. **Clone the repository**:

   ```bash
   git clone https://github.com/krishnakumar51/nlp-project.git
   cd nlp-project
   ```

2. **Set up Python environment**:

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

3. **Install as package**:

   ```bash
   pip install -e .
   ```

## Data Management with DVC

DVC is used to version datasets and preprocessing pipelines:

* **Initialize DVC**:

  ```bash
  dvc init
  ```
* **Run pipeline**:

  ```bash
  dvc repro
  ```
* **Push data**:

  ```bash
  dvc push
  ```

## Training and Evaluation

Hyperparameters are defined in `params.yaml`. Train and evaluate the model:

```bash
make train        # runs training pipeline
make evaluate     # runs evaluation metrics
```

Results and metrics will be stored in `models/` and `reports/`.

## API Service

The Flask application serves the model for inference:

```bash
FLASK_APP=flask_app/app.py flask run --host=0.0.0.0
```

Send POST requests with text input to `/predict` for model predictions.

## Deployment

Build and push Docker image:

```bash
docker build -t nlp-project:latest .
```

Apply Kubernetes manifest:

```bash
kubectl apply -f deployment.yaml
```

## Testing

Run unit and integration tests with tox:

```bash
tox
```

## Dependencies

Key Python libraries:

* `scikit-learn` for ML algorithms
* `transformers` for state-of-the-art NLP models
* `pandas`, `numpy` for data processing
* `Flask` for serving
* `DVC` for data/version control

See `requirements.txt` for full list.

## Contributing

1. Fork the repository
2. Create a new branch: `git checkout -b feature/your-feature`
3. Make your changes
4. Run tests: `tox`
5. Submit a pull request

Please adhere to coding standards and write tests for new functionality.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
