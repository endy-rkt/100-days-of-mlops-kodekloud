# Day 25: Register, Version, and Manage Model Lifecycle

**subject**

***

The xFusionCorp Industries ML platform team needs two trained candidates promoted through the **MLflow Model Registry** so the ops side can track which model version is serving production traffic. Both runs already exist in the `fraud-detection` experiment. Your task is to register both as versions of a new `fraud-detector` model, add a model-level description, and assign `challenger` and `champion` aliases—all through the MLflow UI.

1. The MLflow tracking server is already running on port `5000` and two runs are pre-populated in the `fraud-detection` experiment: a `baseline` run (`n_estimators=100`, `max_depth=5`, `f1_score=0.80`) and an `improved` run (`n_estimators=200`, `max_depth=10`, `f1_score=0.89`). Both runs can be opened via the **MLflow UI** button → `fraud-detection` experiment.
2. Using the MLflow UI, reach the end state below. The order (baseline first, improved second) matters because MLflow assigns version numbers sequentially within a registered model.
   * A registered model named **`fraud-detector`** exists in the Model Registry.
   * The registered model carries a non-empty description that references the word `fraud` (any phrasing; for example `Fraud detection model for xFusionCorp transactions`).
   * **Version 1** of `fraud-detector` is the baseline run and carries the alias **`challenger`**.
   * **Version 2** of `fraud-detector` is the improved run and carries the alias **`champion`**.

> The result can be confirmed by opening **Model registry** → **fraud-detector** in the MLflow UI. Two versions are listed, the description is shown at the top of the model page, and the alias column (or the Aliases field on each version) indicates `challenger` on v1 and `champion` on v2.

***

https://mlflow.org/docs/latest/ml/model-registry/tutorial/

https://medium.com/@faizulkhan56/mastering-mlflow-model-registry-a-complete-hands-on-guide-1309beeac333

* Check Mlflow

![](assets/uyC1AOCgBzWHosvZcPo-vmaa0RgU8rqpalp9R70R4PY=.png)

![](assets/UMaCNZgWeZgkixX3Ndcstlfpee15mU90-L5fzSCw7vI=.png)

* Register the two runs

![](assets/HgOxXDdD6uM5zILOnLDw6VlQhUOegjyKcj2R9lf54LE=.png)

![](assets/jINp1dVKOVx878tDBMkXytATrZzm-M6x9FSJim3JnNE=.png)

* Add alias in model registry

![](assets/ixH6aAAyPAYbR2zH03vaxH37_Q1rrxvsKXjRtczuiVA=.png)

![](assets/5C0oZ0BZkbAgg3vRKX9DojEa8SZYRGqbct7zFW4rJHA=.png)

![](assets/LlaJVCe1754KCWDlYUcbavjc_jC7tyJUv2d025L2n1Q=.png)

* Set the two model

![](assets/kVHeHaNKovmzxBfsQc_xgCoSGBSbblpCmfJdHRPwweg=.png)

