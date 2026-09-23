<h1 align="center">Filipp Lotsmanov</h1>

<p align="center">
  Computer vision and sequence models — and the pipelines that train, serve and retrain them.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-1c1c1c?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Go-1c1c1c?style=flat-square&logo=go&logoColor=white" alt="Go">
  <img src="https://img.shields.io/badge/PyTorch-1c1c1c?style=flat-square&logo=pytorch&logoColor=white" alt="PyTorch">
  <img src="https://img.shields.io/badge/FastAPI-1c1c1c?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI">
  <img src="https://img.shields.io/badge/Airflow-1c1c1c?style=flat-square&logo=apacheairflow&logoColor=white" alt="Apache Airflow">
  <img src="https://img.shields.io/badge/Docker-1c1c1c?style=flat-square&logo=docker&logoColor=white" alt="Docker">
</p>

<p align="center">
  <sub>Breda, Netherlands · open to an ML engineering internship</sub>
</p>

<p align="center">
  <img src="assets/demo.gif" width="640" alt="Predicting an off-screen pedestrian's position from their shadow">
</p>

---

## About

Third-year Applied Data Science & AI at Breda University of Applied Sciences. I build segmentation
and gesture models, and the infrastructure around them — Airflow, Azure ML, FastAPI, Docker. Python
is my main language, Go for concurrent data work.

Most of these were built for external clients or to hackathon deadlines; two are solo. Every number
below names the set it was measured on, and each repo is as explicit about what the project does not
do as about what it does.

---

## Projects

| Project | What it is | Result |
|---|---|---|
| **[root-inoculation-mlops](https://github.com/filipp-lotsmanov/root-inoculation-mlops)** | U-Net root segmentation with a correction-driven retrain loop and two promotion gates · team capstone for NPEC | **0.8371 F1** on 20,512 held-out patches |
| **[autonomous-root-inoculation](https://github.com/filipp-lotsmanov/autonomous-root-inoculation)** | Segmentation and a PID controller driving an Opentrons OT-2 pipette · individual | **10.7% sMAPE**, down from 37.6% |
| **[shadow-detection](https://github.com/filipp-lotsmanov/shadow-detection)** | Locating an off-frame pedestrian from their shadow alone · team of three | **BrabantHack 2026 winner** · IoU 0.626 |
| **[go-etl-pipeline](https://github.com/filipp-lotsmanov/go-etl-pipeline)** | Concurrent streaming ETL in Go where every row is accounted for · personal | **2.3 GB through a 4 MB heap** |
| **[sign-language](https://github.com/filipp-lotsmanov/sign-language)** | Real-time NGT fingerspelling in the browser · team of three | Two models routed over one socket |
| **[resume](https://github.com/filipp-lotsmanov/resume)** | LaTeX CV that verifies itself in CI · personal | The build fails if the PDF stops parsing for an ATS |

Two that are worth a minute each. **root-inoculation-mlops** separates registering a model from
promoting it: a candidate enters the registry only if it clears an F1 threshold on frozen held-out
test, and it takes traffic only if it beats whatever is already serving — so a model can register
and still lose promotion. **sign-language** quotes no accuracy on purpose; its pipeline augments
before splitting, so near-duplicate frames leak across train, validation and test, and the numbers
that produces are not worth reporting.

---

## Stack

<details>
<summary>Grouped by what it is used for</summary>

<br>

**Languages** — Python, Go, SQL

**Deep learning** — PyTorch, TensorFlow, Keras, torchvision, Stable Baselines3

**Computer vision** — OpenCV, MediaPipe, U-Net, scikit-image, scipy.ndimage

**Classical ML** — scikit-learn, pandas, NumPy

**Serving** — FastAPI, WebSocket, TorchScript, mixed-precision inference

**Orchestration and MLOps** — Airflow, Azure ML, MLflow, ClearML, Hydra, Prometheus

**Infrastructure** — Docker, Docker Compose, GitHub Actions, Portainer, PostgreSQL, Alembic

**Tooling** — uv, ruff, pytest, Vitest, Sphinx, LaTeX

</details>

---

## Currently

- Calibration and selective prediction on handwritten text recognition — when a vision-language
  model is wrong about a historical manuscript, does it know?
- DVC end to end: data and model versioning, pipelines, experiments, CI with CML.

---

## Education

**BSc Applied Data Science & Artificial Intelligence** — Breda University of Applied Sciences
<br><sub>2024 – expected July 2028 · GPA 8.5 / 10</sub>

Block-based projects with external clients, spanning computer vision, deep learning, reinforcement
learning, NLP, data engineering and MLOps.

---

<p align="center">
  <a href="mailto:lotsmanov.filipp@gmail.com"><img src="https://img.shields.io/badge/Email-1c1c1c?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
  <a href="https://linkedin.com/in/filipp-lotsmanov/"><img src="https://img.shields.io/badge/LinkedIn-1c1c1c?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
  <a href="https://github.com/filipp-lotsmanov/resume/blob/main/resume.pdf"><img src="https://img.shields.io/badge/Resume-1c1c1c?style=flat-square&logo=adobeacrobatreader&logoColor=white" alt="Resume"></a>
</p>
