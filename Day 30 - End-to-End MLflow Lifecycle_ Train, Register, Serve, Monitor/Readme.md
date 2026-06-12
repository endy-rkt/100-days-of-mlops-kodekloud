# Day 30: End-to-End MLflow Lifecycle: Train, Register, Serve, Monitor

The xFusionCorp Industries MLOps team needs the `fraud-detection-v2` candidate promoted all the way from the tracking server to live inference and monitored end to end. The backing stack (PostgreSQL, SeaweedFS, MLflow tracking server, three candidate runs) is already in place. Your task is to cover the remaining lifecycle work: model promotion, serving, and health monitoring.

1. The infrastructure is fully up: PostgreSQL container `mlflow-db` on port `5432`, SeaweedFS on ports `8333` (S3 API) and `8888` (Filer UI), MLflow tracking server on port `5000` with the PostgreSQL backend and the `mlflow-artifacts` S3 bucket. The `fraud-detection-v2` experiment contains three candidate runs (`baseline`, `improved`, `regression`) with logged `f1_score` metrics. The **MLflow UI** and **SeaweedFS Filer** buttons at the top of the lab can be opened to view each web UI.
2. The complete end state requires the following.
   * A registered model named **`fraud-detector-v2`** exists in the MLflow Model Registry.
   * A **`champion`** alias on that model points at the version sourced from the `fraud-detection-v2` run with the **highest**`f1_score`.
   * An `mlflow models serve` process listens on port `5001`, serving the champion version (`--env-manager=local` is the supported choice for the lab). Export `MLFLOW_TRACKING_URI=http://localhost:5000` in the serving shell so the `models:/` URI can be resolved against the tracking server. The tracking server proxies the model download from SeaweedFS itself, so no S3 credentials are needed in the serving shell.
   * The served endpoint returns `200` on `GET /health`.
   * A shell script at `/root/code/monitor.sh` exists, is executable, probes the served model's `/health` endpoint once, and exits with status `0` when the endpoint is healthy.
3. The top run can be identified either through the **MLflow UI** Compare view or with a one-off `MlflowClient.search_runs()` call—whichever is preferable. The registration and alias assignment are likewise available from the UI (Models tab) or the SDK.

> `mlflow models serve` is long-running; start it in the background, and ensure that the new process is listening on port `5001` before writing the monitoring script.**subject**

***

The xFusionCorp Industries MLOps team needs the `fraud-detection-v2` candidate promoted all the way from the tracking server to live inference and monitored end to end. The backing stack (PostgreSQL, SeaweedFS, MLflow tracking server, three candidate runs) is already in place. Your task is to cover the remaining lifecycle work: model promotion, serving, and health monitoring.

1. The infrastructure is fully up: PostgreSQL container `mlflow-db` on port `5432`, SeaweedFS on ports `8333` (S3 API) and `8888` (Filer UI), MLflow tracking server on port `5000` with the PostgreSQL backend and the `mlflow-artifacts` S3 bucket. The `fraud-detection-v2` experiment contains three candidate runs (`baseline`, `improved`, `regression`) with logged `f1_`

***

https://mlflow.org/docs/latest/genai/serving/

* Check mlflow

![](assets/i5g0pfvgHjAw3nQ4P37ARkUJ3BuMnsklTOxGE7rUQcI=.png)

![](assets/KqsalZ9txovMeP83M7V7xurpF2w8s8nElrnR2pQ3B7A=.png)

* Register the champion model

![](assets/raQ3-ydDqdwgf_ikd54Esrn7a4KkQ7ObmTb90UPqS0M=.png)

* Add alias

![](assets/Fo8Nqdst73mOaMQb0d-1z_xI2LPQWsTItG6hJhpKBjs=.png)

![](assets/TjfY73Mt0M-Biua5JXu1FifZ3tZActzisgBhPPpv3s0=.png)

* Serving the model

![](assets/T1lykNCJmXk8NuZdXjNWktefgPgDRblYF8h4mrKL1Uo=.png)

![](assets/F2FkODfrroN8w9_vogPIRXBTgLE81HLqD5qkCxfMOyA=.png)

* Run and check

![](assets/i82eEjE8WjvMOEpaOL5PBLixSgNwEAnkBK8zPcY2cDI=.png)

![](assets/JCO8wxmcVeXwOk_6GjS33MG_PkwEZJkGPLJZVjfxTQw=.png)

![](assets/dx0SKcZhYxvim5d6PIr0wqn8Vh2rvV-TysQuebgbVGM=.png)





