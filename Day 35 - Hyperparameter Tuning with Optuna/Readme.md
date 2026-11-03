# Day 35: Hyperparameter Tuning with Optuna

**suject**

***

The xFusionCorp Industries ML platform team tunes fraud-detection hyperparameters with Optuna and inspects the full search in the MLflow Compare view. A draft tuner exists at`/root/code/fraud-detection/src/models/tune.py`, but the search optimises in the wrong direction and no trials ever land on the tracking server. Your task is to correct the tuner so each of the 20 trials is visible in MLflow and the saved best configuration is actually the highest-F1 candidate.

1. The MLflow tracking server is already running on port`5000`. The**MLflow UI**button at the top of the lab can be opened to confirm—the dashboard loads with an empty`hyperopt-tuning`experiment.
2. The project layout under`/root/code/fraud-detection/`:
   * `data/train.csv`– The same 200-row synthetic binary-classification dataset Day 34 uses (imbalanced roughly 70 / 30).
   * `src/models/tune.py`– The Optuna tuner scaffold. Fold iteration, metric averaging, Optuna study creation, and YAML persistence are already wired; corrections are required.
   * `configs/`– Where`best_params.yaml`is written after the search completes.
3. Open`src/models/tune.py`in the VS Code editor, correct every issue that keeps the search from meeting the release checklist, save, and run the script once.
4. The end state must include:
   * At least 20 runs exist in the`hyperopt-tuning`experiment on MLflow. Every run carries`params.n_estimators`,`params.max_depth`, and`metrics.f1_score`.
   * A YAML file at`/root/code/fraud-detection/configs/best_params.yaml`with exactly two keys:`n_estimators`(integer in the range`[50, 500]`) and`max_depth`(integer in the range`[3, 20]`).
   * The Optuna study is directed such that`best_params`corresponds to the highest-F1 trial in the search space – Not the lowest.

***

https://optuna.org/

https://github.com/optuna/optuna

https://medium.com/@mustafacavussoglu/optimizing-lightgbm-using-optuna-and-mlflow-f426e52e4871

* Check the existing work

![](assets/potNYElvmebJUUtpsvjNWcDm8StT76CPnlfLa_DLTmU=.png)

![](assets/7ZOnSD3oFPEou86Dpta7ByIqh1psLCVuuaTBfsrr08k=.png)

![](assets/ia8su0kuu9_8KsJEVGkcTBxg-eQjcJd0qtdjGscy8GU=.png)

* Check the errors

Link mlflow to the object 

![](assets/SLTPLoDGXe0bAtlesNtelHp-XDD_Hb-gn_2g982fu1A=.png)

Take the max not the min

![](assets/fhHbUINv8pLWr0j5gXwX3LR7ux2pL_Jh4XvcRWc0m2w=.png)

* Run and check

![](assets/1_DBqN_AWId3mmC3G_NULc091SVLFZxhMz8355OeRcE=.png)

![](assets/NLYKf2MXRcj9K9C7osBSNc6fut04ZtYcI8sHjQX1wWg=.png)

![](assets/E_K8FYelmyaEO0dqza0PwFU3ZgWiyMEe4TW4Rj-7xlQ=.png)

![](assets/7zMHtFod0LzEFIDcjHLskZFeNvHE6yIaHJ9MQFKCb3Y=.png)
