# Day 23: Search and Query MLflow Runs

**subject**

***

A xFusionCorp Industries data scientist has accumulated ten runs in the `fraud-detection` MLflow experiment. Your task is to triage those runs via the **MLflow UI**: mark the single best-performing candidate as the shortlisted model, and flag every clearly under-performing run for removal.

1. The MLflow tracking server is already running on port `5000`, and the `fraud-detection` experiment has been pre-populated with ten runs. The runs can be viewed via the **MLflow UI** button → `fraud-detection` experiment.
2. Using the MLflow UI, complete the triage below. The end state is what is tested—the path taken through the UI is not.
   * **Shortlist the best candidate.** Among all runs where `metrics.f1_score > 0.85`, the single run with the highest `f1_score` must carry a run-level tag: key `review-status`, value `shortlisted`.
   * **Reject the under-performers.** Every run where `metrics.f1_score < 0.75` must carry a run-level tag: key `review-status`, value `rejected`.
3. The other runs (those in the 0.75 ≤ f1 ≤ 0.85 band, and the second-best shortlisting candidate) must carry no `review-status` tag at all.

***

* Access mlflow

![](assets/6HNLX-qu5-JT0ENn15GxGkCFiX6QujvvorfPo74GDto=.png)

* check the runs

![](assets/0CzgbT0QUaO--wzEAIUJPBwtzFczwmL1pS0FN70eBZY=.png)

* shortlist the best candidate

![](assets/Miw59kgIZTdRH6MEv_7DA6ShZimD5EPF_xGlA3bRRdw=.png)

* Add tag for the best candidate

![](assets/cqis5imfWmiGRq392wkvHYjuYe1eXc9sRgWMS95m-XU=.png)

![](assets/mLr6F3HsDlGJAO-KY9mnQaG2I8k4sEhsK8_nLrjg6WQ=.png)

* add tag for under performance runs

![](assets/aQnKveH-b7NSwyNo-h8eSRLgLTpzs9v8eGuuKpUMpSM=.png)

