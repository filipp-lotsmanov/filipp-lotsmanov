Third-year Applied Data Science & AI student at Breda University of Applied Sciences, working on
computer vision, sequence models and the infrastructure that serves them.

Every number below is stated with where it came from. Held-out test scores, competition
leaderboards and preserved training logs are labelled as such, and the projects document what
they cannot do alongside what they can.

---

<p align="center">
  <img src="assets/shadow-detection-demo.gif" width="640" alt="Off-screen pedestrian localisation from shadow imagery">
</p>

---

## Projects

| Project | Type | What it demonstrates | Result |
|---|---|---|---|
| [root-inoculation-mlops](https://github.com/filipp-lotsmanov/root-inoculation-mlops) | Team capstone | Full lifecycle: train, serve, monitor, retrain from user feedback | 0.8371 F1 on held-out test (20,512 patches; training log preserved in-repo) |
| [autonomous-root-inoculation](https://github.com/filipp-lotsmanov/autonomous-root-inoculation) | Individual | Segmentation driving a physical robot; PID and RL control | 37.6% to 10.7% sMAPE (Kaggle private leaderboard) |
| [shadow-detection](https://github.com/filipp-lotsmanov/shadow-detection) | Team of 3 — BrabantHack 2026 winner, DEMCON Deep Tech track | Decomposed regression targets, hand-crafted feature fusion | Winning submission scored IoU 0.626 (hidden test set) |
| [go-etl-pipeline](https://github.com/filipp-lotsmanov/go-etl-pipeline) | Personal | Concurrent streaming ETL with full record accounting | 2.8–5.2 MB heap over a 2.3 GB, 27.6M-record file at ~41k records/sec |
| [sign-language](https://github.com/filipp-lotsmanov/sign-language) | Team of 3 | Real-time dual-model serving over WebSocket | Two-model routing on MediaPipe landmarks; see limitation below |

<details>
<summary><b>root-inoculation-mlops</b> — MLOps platform for plant root segmentation</summary>

<br>

Built for the Netherlands Plant Eco-phenotyping Centre as a five-person capstone. A U-Net segments
root tissue; the platform around it trains, serves, monitors and retrains that model when
researchers correct its predictions.

**My scope:** Airflow orchestration and the Azure ML job layer, the feedback-to-retraining
flywheel, the champion-challenger promotion gate, most of the `cv-pipeline` package, and an equal
share of the backend and infrastructure. The frontend was built by teammates.

**Result:** 0.8371 F1 / 0.7199 IoU on a held-out test set of 20,512 patches. Data is split at
source-image level before patching, so overlapping patches cannot straddle the boundary. The
training log for that run is committed under `docs/evidence/`.

**Limitation:** the Azure and on-premise environments were provisioned for a university project and
have been decommissioned. Their definitions are preserved in `infra/`, but the local Docker Compose
stack is the reproducible path.

</details>

<details>
<summary><b>autonomous-root-inoculation</b> — Segmentation to robot actuation</summary>

<br>

Individual project. U-Net segmentation locates root tips in petri dish images; skeletonisation and
geodesic distance measure root length; an affine transform maps pixels to robot coordinates; a PID
controller drives an Opentrons OT-2 pipette to each target.

**Result:** 37.6% to 10.7% sMAPE on the Kaggle private leaderboard. The improvement came from
deleting machinery rather than adding it — adaptive dish detection and watershed splitting were
solving problems this dataset did not have.

**Limitation:** the PID and PPO controllers were measured on different simulators (a theoretical
velocity model versus PyBullet), so their error figures are not directly comparable. The RL
training runs were submitted to a university ClearML server and the plots were not preserved.

</details>

<details>
<summary><b>shadow-detection</b> — Off-screen pedestrian localisation</summary>

<br>

Winning entry in the BrabantHack 2026 DEMCON Deep Tech track, with Oleksii Krasnoshtanov and Danil
Sysenko. Given a road scene where a pedestrian is out of frame but their shadow is not, predict the
bounding box where they would be standing.

**My scope:** the three-head decomposed-target architecture — rather than regressing raw box
coordinates, a classifier picks the side of frame and a regressor learns continuous offsets from
that edge — plus 19 hand-crafted geometric features, flip-aware augmentation, and the
test-time-augmentation inference path. Teammates ran complementary models; the submitted result was
a weighted blend of all three.

**Result:** the team submission scored IoU 0.626 on the hidden leaderboard test set.

**Limitation:** the direction head (walking into versus out of frame) does not work and is
documented as a dead end, with a likely cause recorded. Training data is entirely synthetic, so
real-world generalisation is untested. There is no local ground-truth test split.

</details>

<details>
<summary><b>go-etl-pipeline</b> — Concurrent streaming ETL</summary>

<br>

Personal project. A staged pipeline in Go — source, validate, transform, sink — connected by
channels, loading CSV into PostgreSQL with memory independent of file size.

**Result:** a flat 2.8–5.2 MB heap across a 2.3 GB, 27.6M-record file at roughly 41,000
records/sec, insert-bound. Enrichment runs 4.76x faster across a goroutine worker pool than
single-threaded at the shipped settings.

The part worth reading is the record accounting: every row read is attributed to the stage that
consumed it, and a run whose ledger does not balance exits non-zero rather than reporting success.
Re-runs are idempotent through a fingerprint unique index.

**Limitation:** the higher 5.7x speedup figure in the benchmarks section was measured with a source
constant raised, so reproducing it requires editing and rebuilding.

</details>

<details>
<summary><b>sign-language</b> — Real-time NGT fingerspelling recognition</summary>

<br>

Browser app teaching the Dutch Sign Language fingerspelling alphabet, with Oleksii Krasnoshtanov
and Danil Sysenko. MediaPipe extracts hand landmarks in the browser; frames stream to a FastAPI
backend over WebSocket; static and dynamic letters route to different models.

**My scope:** the model architectures and the serving path. A ResidualMLP classifies the 24 static
letters from a single 63-dimensional landmark vector; a bidirectional LSTM classifies J and Z from
30-frame sequences. Per-letter routing dispatches to whichever applies.

**Limitation:** the training pipeline augments before splitting, so jittered copies of the same
source frame appear in train, validation and test. The validation accuracies this produces are
inflated by near-duplicate leakage and are not reported here. No NGT fingerspelling dataset existed,
so the data was recorded by team members who are not fluent signers.

</details>

---

## Stack

<details>
<summary>Grouped by what it is used for</summary>

<br>

**Languages** — Python, Go, SQL

**Deep learning** — PyTorch, TensorFlow, Keras, torchvision, Stable Baselines3

**Computer vision** — OpenCV, MediaPipe, U-Net, scikit-image, scipy.ndimage

**Classical ML** — scikit-learn, pandas, NumPy

**Serving** — FastAPI, WebSocket, TorchScript, mixed-precision inference, Next.js

**Orchestration and MLOps** — Airflow, Azure ML, MLflow, ClearML, Hydra, Prometheus

**Infrastructure** — Docker, Docker Compose, GitHub Actions, Portainer, PostgreSQL, Alembic

**Tooling** — uv, ruff, pytest, Vitest, Sphinx

</details>

---

## Currently

- Completing a calibration and selective-prediction study on handwritten text recognition,
  comparing a TrOCR baseline against a LoRA fine-tuned vision-language model on historical
  manuscripts.
- Working through DVC end to end — data and model versioning, pipelines, experiment tracking, and
  CI integration with CML.

---

[lotsmanov.filipp@gmail.com](mailto:lotsmanov.filipp@gmail.com) · [LinkedIn](https://linkedin.com/in/filipp-lotsmanov/) · [Resume](https://github.com/filipp-lotsmanov/resume/blob/main/resume.pdf)
