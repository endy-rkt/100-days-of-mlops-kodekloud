# Day 40: Production Training System: Tracking, Tuning, and Model Selection

**subject**

***

The xFusionCorp Industries ML platform team ships a full fraud-detection training pipeline—data validation, Optuna tuning across two model families, model selection against a release threshold, Model Registry registration with a release-lane alias, and a consolidated training report—all wired together behind a single`make train-pipeline`command. The pre-staged system does not currently run end-to-end: each`make train-pipeline`invocation surfaces a wiring issue, and the integration across the`Makefile`,`src/select_model.py`, and`src/register.py`needs attention before the release checklist passes. Your task is to correct the wiring so`make train-pipeline`runs cleanly end-to-end, the MLflow Model Registry holds a`fraud-detector`version under the`staging`alias, and`reports/training_report.json`aggregates every upstream artefact.

1. The MLflow tracking server is already running on port`5000`. The**MLflow UI**button at the top of the lab can be opened to confirm—the dashboard loads with an empty`fraud-detection-tuning`experiment.
2. The project layout under`/root/code/fraud-detection/`:
   * `data/train.csv`– The 200-row synthetic binary-classification dataset the rest of the Training section uses.
   * `src/validate_data.py`– Schema + null-check gate. Writes`reports/validation_status.json`. Correct.
   * `src/tune.py`– Runs 10 Optuna trials across RandomForest and GradientBoosting, each logged as an MLflow run tagged with`model_type`+`params.{n_estimators,max_depth}`+`metrics.f1_score`+ the fitted model artefact. Correct.
   * `src/select_model.py`– Picks the winning run by the training metric and writes`reports/selection.json`. Needs attention.
   * `src/register.py`– Registers the selected run's model as`fraud-detector`and assigns the release-lane alias. Needs attention.
   * `src/report.py`– Aggregates every upstream artefact into`reports/training_report.json`. Correct.
   * `Makefile`–`train-pipeline`target runs the five stages in order. Needs attention.
3. Run`make train-pipeline`from`/root/code/fraud-detection/`to surface each issue in turn. Open the offending file in the VS Code editor, correct the wiring, and re-run until the pipeline completes without non-zero exit.
4. The end state must include:
   * `make train-pipeline`completes without non-zero exit.
   * The`fraud-detection-tuning`MLflow experiment carries at least five trial runs, each with`metrics.f1_score`.
   * `reports/selection.json`,`reports/validation_status.json`, and`reports/training_report.json`are all present. The training report carries`best_model`,`best_params`,`metrics`,`total_trials`, and`validation_status`keys;`validation_status`is`"ok"`and`total_trials`is an integer ≥ 5.
   * The MLflow Model Registry (**MLflow UI**→**Models**) shows a`fraud-detector`registered model with at least one version. That version carries the`staging`alias and no`production`alias.

> Run`make train-pipeline`once against the scaffold as-is; the first wiring issue surfaces immediately. Each subsequent re-run reveals the next stage's problem. Every fix is a one-line edit in one of the three files listed above.

***

* Check the current work

![](assets/3S2ku84QcdxgyEW1yeiRcxt3k558N5h9hj7ZXL23NWo=.png)

![](assets/u8aNO0gYqDwV_CvkMbO1KIGsqr0wjv7XKvWrbP6FcQs=.png)

![](assets/1iU-RwDgQ34P7X8TzQ6zj7h74ltK-bc5-QE3eufw6I8=.png)

![](assets/LuVvyNjng0Bq4v35-QTyeFI59lfm6wVrlWlUco82ejg=.png)

![](assets/gFqyPZL6J5FGWWjP3hgpqmTOh8E_jYq0Pcuo8yL5cOQ=.png)

![](assets/FynXwQw0cZIqf-A1uwjuUp6UHMls_kaFW-9UbwHwCK0=.png)

![](assets/NrLVGxwkYUfSDFl7ywajklnsz7NFvjJSFGpF0L8eoj0=.png)

![](assets/Lvlx6-MktTLK4D8bHETCYWoSar78JJCXcGEp8RYlTs8=.png)

![](assets/AfNq_3QFKRqeiXvFcIHZJvwk7ixkpZF0B7HIxA1lZKQ=.png)

![](assets/Ug_rPQ0tRYUTkmznGtoOCA5VSFPZRVaiY2KQjczWHTA=.png)

![](assets/93YxJLjjaJfPVeTzAAMr8qJm00Pui_2TiLDJl2bq8QI=.png)

![](assets/Dm5tb3P3WcgM3Kx3F72_a_ba7E6yepWi8rrtwzOSjis=.png)



* Check errors

in select\_model.py replace accuray to f1\_score

![](assets/kO9iOMVAngWck0FEDOr2ndRwJY2SBKfsjaK3qiatBZo=.png)

in the makefile, fix order

![](assets/0hf0ecd8jbOBpZGq27FcN9dolmu6DFNhs6Rv2Xp1VV8=.png)

fix the alias in register.py

![](assets/UELXsqhMOsL8L1brV-_-BBNnCIvGgbE-lcUHQ2V1wZ8=.png)

* Run and check

![](assets/jMDQGOCMs67WtB2JZ9pUMnpeGkAOEwebsOd7fRnbGts=.png)

![](assets/BCcqxQEpJ1qmxGZqXDqNXMOWuh_4VoLxnAZH0v03JwE=.png)

![](assets/iOxNU5A2tFNmL7OttLbZJGVLd8HsBjbphW0TqSU_oEc=.png)
