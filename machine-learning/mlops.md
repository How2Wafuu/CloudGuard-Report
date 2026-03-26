# ML Deployment & MLOps

The ML lifecycle in CloudGuard AI is designed to support traceability, controlled promotion, and repeatable retraining.

<figure><img src="../.gitbook/assets/ML Deployment + MLOps.png" alt=""><figcaption></figcaption></figure>

## MLOps Pipeline

1. **SOC outcomes become feedback.** True-positive and false-positive decisions from analysts are stored as labeled cases.
2. **Training data is prepared from hot data and labeled cases.** Recent searchable data from the HQ hot window is combined with investigation outcomes.
3. **The feature pipeline is versioned.** This ensures that feature transformations are consistent across training and inference.
4. **Training runs on HQ GPU infrastructure.** Training jobs may be scheduled regularly or triggered on demand.
5. **MLflow tracks experiments.** Parameters, metrics, and artifacts are recorded for each training run.
6. **Models are promoted through a registry.** Candidate models move from **staging** to **production** after evaluation.
7. **Artifacts are stored in MinIO Model files, and checkpoints and related artifacts are kept in the HQ object store.**
8. **CI/CD builds the inference container.** The selected model is packaged with the inference service as a deployable Docker image.
9. **Inference API is deployed as a stateless service.** The FastAPI + PyTorch service runs behind a load balancer and can be replicated horizontally.
10. **Monitoring tracks model and system health.** Key signals include latency, error rate, CPU/GPU usage, score distribution, and drift.
11. **Alerts can trigger retraining or rollback.** When model drift or degraded performance is detected, retraining can be initiated. If needed, rollback is performed by switching the production registry tag back to a previous model version.

This workflow makes the ML subsystem operationally manageable rather than treating the model as a one-time experiment. It also supports reproducibility, staged release, and controlled recovery.
