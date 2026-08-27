# Raphael Farodoye

**Data Scientist — production ML, applied GenAI, MLOps.** MSc in Computer Science (Machine Learning and AI) at UFSM. Background in Economics.

I build models that have to survive contact with a business decision. Most of the work below is organised around one question: what does it cost when the model is wrong, and does the system behave sensibly when it is unsure?

---

## Selected work

### Credit-Risk Decisioning on 6.3M Payment Transactions
[`FRAUD_DETECTION`](https://github.com/Raphlawren/FRAUD_DETECTION)

Not "is this transaction fraud," but "given a calibrated probability and the cost of each mistake, do I approve, block, or route for review."

- **PR-AUC 0.9425** on a sealed 1.9M-transaction test set with a 0.13% event rate. Reported instead of accuracy, which at that base rate tells the reader nothing.
- Operating threshold chosen by **minimising expected loss** under a 10:1 missed-fraud to false-alarm cost ratio, not by maximising F1: **95.3% recall at 66.9% precision** at t = 0.114. The cost ratio is a config input, so risk can move the operating point without retraining.
- Isotonic calibration on a held-out slice so the probabilities driving that threshold mean something, and SHAP attribution so a single flagged decision can be explained to an analyst or auditor.

`XGBoost` · `Optuna` · `scikit-learn` · `SHAP`

### Predicting Evolving 2D Star-Shaped Polygons Using Time Series
[`2D-Shape-prediction`](https://github.com/Raphlawren/2D-Shape-prediction) — with Célio Trois (UFSM) · **[CONFIRM STATUS: under review / accepted / published, IEEE Access]**

A radial framework for forecasting how a 2D boundary moves over time: cast 360 rays from a fixed origin, turn each ray into its own univariate series of radial distances, forecast, and reconstruct the boundary.

- Validated on three datasets: two synthetic controls and a **real Posidonia oceanica seagrass meadow near a Spanish seaport, 1994 to 2022**, with the final year held out.
- Benchmarked against ARIMA, linear regression, a moving average and a persistence baseline under one evaluation protocol. Tuned Prophet with trend clipping gave the **lowest radial error of every non-persistence model (MAE 0.0119 km)**.
- Persistence still edges the model on polygon IoU, and the write-up says so, along with where the method breaks: rays are forecast independently with no angular smoothing, and accuracy degrades when the shape translates rapidly away from the origin.

`Prophet` · `Shapely` · `statsmodels` · `QGIS` · `GeoPandas`

### Hybrid Log Classification with an LLM Fallback Tier
[`log_classification_hybrid_model`](https://github.com/Raphlawren/log_classification_hybrid_model)

Three-tier routing that sends predictable records to deterministic rules, well-represented cases to a classifier over sentence embeddings, and only genuinely ambiguous ones to an LLM call. Keeps per-record cost down while holding **0.99 accuracy and 0.99 weighted F1** on a held-out split. Served as a FastAPI batch service.

`Sentence Transformers` · `scikit-learn` · `Groq / Llama 3.3` · `FastAPI`

### Document Question-Answering with RAG
[`Building-Chatbot-Using-LLAMA-and-RAG`](https://github.com/Raphlawren/Building-Chatbot-Using-LLAMA-and-RAG)

Upload a PDF, ask questions against it. Chunking with overlap, MiniLM embeddings into ChromaDB, Maximum Marginal Relevance retrieval to cut redundant context before generation. Containerised, with a browser chat interface.

`LangChain` · `ChromaDB` · `LLaMA via IBM watsonx.ai` · `Flask` · `Docker`

### Benchmarking Five Data Technologies for ML Pipelines
[`Database-Management-System-Tools`](https://github.com/Raphlawren/Database-Management-System-Tools)

One dataset of 658,877 rows and 202 features, five technologies, a constant workload, and results that can be read side by side.

- LASSO cut the feature set **77.8% down to 42 features while accuracy held at 99.95%**, against 84.13% reduction for a filter method and a wrapper method that needed 25 minutes to run.
- Retrieval latency measured end to end: **0.018s** from a Feast feature store against **0.251s** for a Pinecone ANN query.
- Every run tracked in MLflow with DagsHub, so the comparison is reproducible rather than asserted.

`MLflow` · `Feast` · `Pinecone` · `DagsHub`

**Also here:** [PySpark ETL and Spark SQL pipelines](https://github.com/Raphlawren/customer-transactions-pyspark) · [CNN plant disease classifier deployed on GCP](https://github.com/Raphlawren/Potato-Disease) · [Case-based reasoning for chronic kidney disease staging](https://github.com/Raphlawren/Chronic-Kindey-Disease-Prediction-with-CASE_BASED-REASONING)

---

## In production

At **Agromai** I owned the machine learning lifecycle for a satellite-based pasture classification system running over thousands of georeferenced fields in Brazil.

- Cut false positives **31.7%** with confidence-gated inference: a field was only assigned to the high-consequence class above 80% model confidence, otherwise it fell through to the next most likely class. Misclassifying a healthy crop has a direct financial cost to a farmer, so the trade was deliberate.
- Evolved the production model from XGBoost to LightGBM after monitoring real false-positive rates, and promoted the new version only once the gain was measurable. MLflow held the comparison.
- Traced a failing model back to the source data rather than the method: reviewed NDVI and EVI2 curves field by field, found sowing and harvest dates recorded incorrectly, built a Streamlit tool so the team could fix them, then automated the correction.

---

## Stack

| | |
|---|---|
| **Languages** | Python, SQL, Bash |
| **ML** | scikit-learn, XGBoost, LightGBM, Optuna, SHAP, Prophet, sktime, ROCKET |
| **Deep learning** | TensorFlow/Keras, PyTorch, CNNs, LSTM/GRU, attention |
| **LLMs and GenAI** | LangChain, RAG, ChromaDB, Pinecone, Sentence Transformers, Hugging Face Transformers, Groq/Llama 3.3, IBM watsonx.ai, OpenAI Whisper |
| **Serving and MLOps** | FastAPI, Flask, Docker, Celery, Redis, ONNXRuntime, MLflow, DagsHub |
| **Data** | PostgreSQL, PostGIS, MySQL, SQLite, Apache Spark (PySpark), Feast |
| **Geospatial** | GeoPandas, Shapely, QGIS, Sentinel Hub API |
| **Cloud** | Google Cloud Platform |

---

## Research

MSc in Computer Science (Machine Learning and AI) at Universidade Federal de Santa Maria, supervised by Professor Célio Trois. Focus on spatio-temporal forecasting and geospatial time series.

Farodoye, R. L., and Trois, C. *Predicting Evolving 2D Star-Shaped Polygons Using Time Series.* **2026**

---

## Contact

[LinkedIn](https://www.linkedin.com/in/raphael-farodoye-81035b28b/) · raphaelfarodoye01@gmail.com · Porto Alegre, Brazil (UTC-3)
