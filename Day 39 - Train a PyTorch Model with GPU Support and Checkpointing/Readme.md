# Day 39:  Train a PyTorch Model with GPU Support and Checkpointing

**subject**

***

The xFusionCorp Industries ML platform team ships fraud-detection models built on a tiny PyTorch network. The training script needs to run on whichever accelerator the host exposes—CUDA GPUs in the production cluster, plain CPU on this lab's nodes—so the same code works on every target. A draft trainer exists at`/root/code/fraud-detection/src/models/train_pytorch.py`, but it assumes CUDA is always present and crashes on the first tensor move, and the device parameter it logs to MLflow is hardcoded. Your task is to make the trainer device-aware and ensure the MLflow run truthfully reports the device it actually used.

1. The MLflow tracking server is already running on port`5000`. The**MLflow UI**button at the top of the lab can be opened to confirm—the dashboard loads with an empty`gpu-training`experiment. PyTorch (CPU build) is baked into the lab image;`import torch`works out of the box. The host does not expose a GPU (`torch.cuda.is_available()`returns`False`).
2. The project layout under`/root/code/fraud-detection/`:
   * `data/train.csv`– The same 200-row synthetic binary-classification dataset the rest of the Training section uses.
   * `src/models/train_pytorch.py`– The trainer scaffold. The two-layer feedforward network, the optimiser, the loss function, the MLflow experiment setup, and the model-persistence call to`models/fraud_model.pt`are already wired; two specific corrections are required.
3. Open`src/models/train_pytorch.py`in the VS Code editor, correct the two problems that keep the trainer from running on this host, save, and run the script once.
4. The end state must include:
   * The script completes successfully and writes a PyTorch state-dict to`/root/code/fraud-detection/models/fraud_model.pt`.
   * One run exists in the`gpu-training`experiment on MLflow, carrying`params.device = "cpu"`and`metrics.final_loss`.
   * No bare`.cuda()`calls remain anywhere in`train_pytorch.py`.

> `torch.cuda.is_available()`returns`True`on GPU hosts and`False`on CPU-only hosts. The idiomatic pattern is to build a single`device = torch.device("cuda" if torch.cuda.is_available() else "cpu")`at the top of training, use`.to(device)`on every tensor and the model, and log`str(device)`to MLflow so the run reports where it actually ran.

***

* Check the existing work

![](assets/c2uR6CoX0DTQbxx3_kyjydQdTi1KSMflmU98Q1CJeRM=.png)

![](assets/Jdeaiq6eoCbf7OcEGQKAZZ30tLudfcOXEL0b7m-Ekf0=.png)

![](assets/fIaHTio09u1wDTtLud0d_vseJJuoxYNYLAyrlV3vADk=.png)

* Fix the code

Add the device check type

![](assets/nWhe2zyiFcWUju-MJztuEhUQ7k4IuiRGWPIeDghwIc4=.png)

Replace cuda to(device)

![](assets/_aBqyM-zwpdIXXP_ru7Sd71CoasFu3-A2EtKnMdV7-k=.png)

* Run and check

![](assets/yHRrwQgIBYwtPyZ6ocEDsAjYOGWrw0HY74hjYd7k7N0=.png)

![](assets/XySiNeZOh6gIXKW5cXseDZTglJil_JoEWj61FePWQGo=.png)
