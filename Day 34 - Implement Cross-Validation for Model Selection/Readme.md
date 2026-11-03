# Day 34: Implement Cross-Validation for Model Selection

**subject**

***

The xFusionCorp Industries ML platform team evaluates fraud-detection candidates with k-fold cross-validation so every candidate is measured on multiple folds of an imbalanced dataset. A draft cross-validation scaffold exists at`/root/code/fraud-detection/src/models/cross_validate.py`, but its report does not match the release checklist and the fold strategy does not preserve the class ratio. Your task is to correct the scaffold so the cross-validation report lands in the expected shape.

1. The MLflow tracking server is already running on port`5000`. The**MLflow UI**button at the top of the lab can be opened to confirm—the dashboard loads with an empty`fraud-detection-cv`experiment.
2. The project layout under`/root/code/fraud-detection/`:
   * `data/train.csv`– A pre-generated 200-row synthetic binary-classification dataset with an imbalanced class split (roughly 70 / 30). Do not regenerate it.
   * `src/models/cross_validate.py`– The cross-validation scaffold. Every concern other than the splitter and the aggregate schema is correctly wired: fold iteration, per-fold metric computation, nested MLflow runs under a parent, JSON persistence, and artefact logging.
   * `reports/`– Where the cross-validation report must land.
3. Open`src/models/cross_validate.py`in the VS Code editor, correct the two problems that keep the report from meeting the release checklist, save, and run the script.
4. The end state must include:
   * A file at`/root/code/fraud-detection/reports/cv_results.json`(absolute path, inside the project's reports directory).
   * That JSON contains exactly these seven top-level keys:`mean_accuracy`,`std_accuracy`,`mean_f1`,`std_f1`,`mean_roc_auc`,`std_roc_auc`,`folds`. Every`mean_*`and`std_*`value is numeric.
   * The`folds`value is a list of five per-fold dictionaries; each carries the keys`fold`,`accuracy`,`f1`,`roc_auc`.
   * The cross-validation splitter is stratification-aware – Each fold preserves the dataset's class ratio.
   * One parent MLflow run in the`fraud-detection-cv`experiment with five nested children (`fold-1`through`fold-5`), each logging the per-fold metrics.

> `StratifiedKFold`is already imported at the top of the scaffold—no new imports are required. The fix is confined to the CV splitter and the aggregate dict.

***

https://scikit-learn.org/stable/modules/cross\_validation.html

https://www.geeksforgeeks.org/python/numpy-std-in-python/

* Check  cross\_validate.py

![](assets/g2sXxA53F5UpDJhnvNeZt2D5y5_b0cRpXYcVaYCiuqI=.png)

![](assets/FWSK3ZZt2unUAyq98U-vdbeoJfNj4GLVyi0pSP1CwO0=.png)

![](assets/7xWvKHvUJ7t-tXtRa0FdfES-UFMaGWCKW2EMycJj7tU=.png)

![](assets/9FgqbF6mp1vhNQ6Ur9zwY-wasSKqRtG46KVU47zcILk=.png)

* Use stratifiedkfold instead of kfold

![](assets/StuD4lyQvRKh2b8yeaE5XCYUfJHcOQspv8Iyu7fy6u0=.png)

* Add standard deviation metrics

![](assets/KuSllkgMgM9eyK_VPeliHrF761K1ktEnus-Ay_IXlvQ=.png)

* &#x20;Run and check

![](assets/-3wGpyHWM3ECdTXFgTEaYrGwUGSrHiy2-kvPeFpzXsY=.png)

![](assets/FXNjh1x2Xx8drqWXYsN042WyLNVsM-WFDVABEvLP9n0=.png)

***

La différence principale réside dans la gestion des classes cibles. **KFold divise les données aléatoirement sans tenir compte des étiquettes, ce qui peut entraîner une représentation déséquilibrée. StratifiedKFold garantit que chaque pli conserve la même proportion d'exemples pour chaque classe que le jeu de données d'origin**

