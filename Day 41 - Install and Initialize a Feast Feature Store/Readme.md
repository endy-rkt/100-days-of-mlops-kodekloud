# Day 41: Install and Initialize a Feast Feature Store

**subject**

***

The xFusionCorp Industries ML platform team is adopting Feast as the feature store for their fraud-detection workflow. The first step is to scaffold a working feature repository with the Feast CLI, apply the starter definitions to the local registry, and confirm everything loads in the Feast UI. Your task is to initialise a new feature repository under`/root/code/`, apply the registry, and verify the empty project loads in the Feast UI.

1. Feast is already installed in the lab image.`feast version`can be run in the terminal to confirm.
2. The target project layout:
   * `/root/code/feature_repo/feature_repo/feature_store.yaml`– The`feast init`scaffold config (provider, registry, online/offline stores).
   * `/root/code/feature_repo/feature_repo/data/registry.db`– Written by`feast apply`from the repo root.
   * `/root/code/feature_repo/feature_repo/feature_definitions.py`– The starter feature definitions Feast ships with the scaffold.
3. The end state must include:
   * The`/root/code/feature_repo/feature_repo/`directory is populated with the`feast init`scaffold.
   * `feature_store.yaml`parses as valid YAML and carries the`project`,`provider`, and`registry`keys.
   * `data/registry.db`exists –`feast apply`completed without error.
   * `feast version`exits zero.
   * The**Feast UI**button at the top of the lab opens a responsive dashboard that lists the scaffold's project.

> `feast ui`is a long-running process; run it in a second VS Code terminal (or append`&`to the command) so the shell remains usable. The UI loads the registry at start-up—start the UI after`feast apply`has written`registry.db`.

***

https://docs.feast.dev/getting-started/quickstart

* Check feast version

![](assets/-cjDu5aDFDBzC84c_6wvq6x52prAo19KiTakf1N7sgM=.png)

* Init feast repo

![](assets/89DjS2V9D8VvaHV_2GjTJT6mMz82Ax-Ozs95Z9Ex9jI=.png)

![](assets/-m2bAINZyA1jhUrcN5gRpYIRiUpGKu0Q323QPr8TMes=.png)

![](assets/SUGoW-hYUF-dC7i9J5Kv8J8IB3hTpTQdGUHb31PK3_M=.png)

* run feast apply 

![](assets/1z2YkH7rc6FBmd_IFXfWe-gmbvS-imz0ct56fRjcrOc=.png)

* Check feast ui

![](assets/DLb1ylmKbzm8Oyk5jz0KHGccbRDDnvsm_u97e9M8_LE=.png)

![](assets/VlyFyFyb73MxacgKzwrVC4X9e9hra_kNjwWqt9F7L2U=.png)
