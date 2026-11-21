# Hit Counter Service - CI/CD Final Project

[![CI workflow](https://github.com/AaliyahLusianti/ci-cd-final-project/actions/workflows/workflow.yml/badge.svg)](https://github.com/AaliyahLusianti/ci-cd-final-project/actions/workflows/workflow.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Python](https://img.shields.io/badge/Python-3.9-brightgreen.svg)](https://www.python.org/)

This repository contains the completed Final Project for the Coursera / IBM course **Continuous Integration and Continuous Delivery (CI/CD)**.

## Project Details

- **Project Name:** Hit Counter Service - CI/CD Final Project
- **Repository:** [ci-cd-final-project](https://github.com/AaliyahLusianti/ci-cd-final-project)
- **Author:** Aaliyah Lusianti

## Description

The project implements an enterprise-grade CI/CD pipeline using **GitHub Actions**, **Tekton**, and **Red Hat OpenShift** for a cloud-native Python Flask Hit Counter RESTful API service.

### Components

1. **RESTful Application:** Flask service implementing endpoints for managing hit counters (`GET /`, `GET /health`, `POST /counters/<name>`, `GET /counters/<name>`, `PUT /counters/<name>`, `DELETE /counters/<name>`).
2. **Continuous Integration (GitHub Actions):** Automated linting with `flake8` and unit testing with code coverage using `nose`.
3. **Tekton Pipeline (Continuous Delivery):** Tekton Tasks and Pipeline running in OpenShift:
   - `cleanup`: Cleans up the shared workspace.
   - `git-clone`: Clones the source repository.
   - `flake8`: Lints the Python codebase.
   - `nose`: Executes unit tests and checks test coverage.
   - `buildah`: Builds container images and pushes to the container registry.
   - `openshift-client (deploy)`: Deploys the application to OpenShift.

## Repository Structure

```text
├── .github/
│   └── workflows/
│       ├── README.md
│       └── workflow.yml               # GitHub Actions CI workflow
├── .tekton/
│   ├── README.md
│   ├── tasks.yml                      # Custom Tekton tasks (cleanup, flake8, nose)
│   ├── pipeline.yml                   # Tekton CI/CD pipeline
│   └── pvc.yml                        # PersistentVolumeClaim definition
├── bin/
│   └── setup.sh                       # Environment setup script
├── service/                           # Flask microservice source code
│   ├── __init__.py
│   ├── routes.py
│   └── common/
├── tests/                             # Unit tests using nose
│   └── test_routes.py
├── screenshots/                       # Evidence screenshots for OpenShift
│   ├── oc-pipelines-console-pvc-details.png
│   ├── oc-pipelines-oc-final.png
│   └── oc-pipelines-oc-green.png
├── cicd-github-validate               # Terminal output of GitHub Actions run
├── oc-pipeline-application-logs       # OpenShift application logs
├── Dockerfile                         # Container build definition
└── requirements.txt                   # Python dependencies
```

## Running Locally

1. Create a Python virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

2. Run linter and tests:
   ```bash
   flake8 service --count --max-complexity=10 --max-line-length=127 --statistics
   nosetests -v --with-spec --spec-color --with-coverage --cover-package=service
   ```

3. Run the service:
   ```bash
   gunicorn --bind 0.0.0.0:8000 service:app
   ```

## License

Licensed under the [Apache License, Version 2.0](LICENSE).
