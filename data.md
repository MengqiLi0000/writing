# Primary Interests

Focus: **machine learning theory, nonparametric statistics, model training, and data systems**.

Settings where standard Euclidean / i.i.d. assumptions are weak: high-dimensional function estimation, structured dependence, irregular geometry, spatial processes, sequences, graphs, and distribution shift

## Nonparametric Statistics / ML Theory

Some topics:

`kernel methods` · `RKHS` · `local polynomial regression` · `splines / GAMs` · `Gaussian processes` · `quantile regression` · `sieve estimation` · `regularized inverse problems` · `bootstrap / uniform inference`

Useful references:

* [Kernel Ridge Regression](https://scikit-learn.org/stable/modules/kernel_ridge.html) — regularized estimation in RKHS.
* [Gaussian Processes](https://scikit-learn.org/stable/modules/gaussian_process.html) — function estimation with explicit covariance structure.
* [statsmodels Nonparametric](https://www.statsmodels.org/stable/nonparametric.html) — KDE / kernel regression.
* [Quantile Regression](https://www.statsmodels.org/stable/generated/statsmodels.regression.quantile_regression.QuantReg.html) — conditional distribution beyond the mean.
* [CVXPY](https://www.cvxpy.org/) — constrained / regularized estimation.

A common form:

```text
argmin_f  empirical_loss(f) + λ · complexity(f)
```

Interest extends to **non-Euclidean ML**: graph-structured data, spatial manifolds, relational dependence, and learning where distance / neighborhood structure is not well represented by ordinary vector geometry.

Reference models / ideas:

[Graph Neural Networks](https://distill.pub/2021/gnn-intro/) · [Geometric Deep Learning](https://arxiv.org/abs/2104.13478) · [Gaussian Processes on structured domains](https://gaussianprocess.org/gpml/)

---

## Model Training

Trained:

* [BERT](https://arxiv.org/abs/1810.04805)
* TF-IDF + Logistic Regression
* Naive Bayes
* Linear / Logistic Regression
* Tree ensembles
* [YOLOv8](https://github.com/ultralytics/ultralytics)
* CNN-based image models

Canonical references:

[XGBoost](https://xgboost.readthedocs.io/) · [ResNet](https://arxiv.org/abs/1512.03385) · [U-Net](https://arxiv.org/abs/1505.04597) · [ViT](https://arxiv.org/abs/2010.11929) · [Llama](https://github.com/meta-llama/llama) · [Qwen](https://github.com/QwenLM/Qwen) · [CLIP](https://arxiv.org/abs/2103.00020) · [LoRA](https://arxiv.org/abs/2106.09685) · [DPO](https://arxiv.org/abs/2305.18290)

---

## Applications

### Financial Data

`time series` · `event streams` · `cross-sectional panels` · `fundamentals` · `macro`

[NASDAQ TotalView](https://www.nasdaq.com/solutions/nasdaq-totalview) · [SEC EDGAR](https://www.sec.gov/edgar) · [FRED / ALFRED](https://alfred.stlouisfed.org/) · [Kenneth French Data Library](https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html) · [Oxford-Man Realized Library](https://realized.oxford-man.ox.ac.uk/)

Methods: state-space models, GARCH, factor models, XGBoost, temporal sequence models, point-in-time feature construction.

### Geospatial Data

`raster` · `vector` · `multispectral` · `SAR` · `climate grids` · `spatiotemporal fields`

[Sentinel-2](https://sentinels.copernicus.eu/web/sentinel/missions/sentinel-2) · [Landsat](https://www.usgs.gov/landsat-missions) · [ERA5](https://www.ecmwf.int/en/forecasts/dataset/ecmwf-reanalysis-v5) · [BigEarthNet](https://bigearth.net/) · [SpaceNet](https://spacenet.ai/datasets/)

Methods: CNN / ViT, XGBoost, Gaussian processes, kriging, spatial kernels, blocked spatial validation.

Tools: [GDAL](https://gdal.org/) · [Rasterio](https://rasterio.readthedocs.io/) · [GeoPandas](https://geopandas.org/) · [xarray](https://docs.xarray.dev/) · [PostGIS](https://postgis.net/)

### Hardware

`video` · `IMU` · `GPS` · `LiDAR` · `device telemetry` · `degradation`

[Waymo Open Dataset](https://waymo.com/open/) · [nuScenes](https://www.nuscenes.org/) · [KITTI](https://www.cvlibs.net/datasets/kitti/) · [NASA C-MAPSS](https://data.nasa.gov/dataset/C-MAPSS-Aircraft-Engine-Simulator-Data/xaut-bemq/about_data)

Methods: YOLO, CNNs, Kalman filtering, tree models, temporal models, survival / degradation modeling.

### Clinical / Sensitive Longitudinal Data

`repeated measures` · `missingness` · `censoring` · `survival` · `privacy constraints`

[MIMIC-IV](https://physionet.org/content/mimiciv/) · [eICU](https://physionet.org/content/eicu-crd/) · [NHANES](https://www.cdc.gov/nchs/nhanes/) · [UK Biobank](https://www.ukbiobank.ac.uk/)

Methods: logistic regression, Cox PH, mixed effects, GEE, XGBoost, doubly robust estimation.

### Language Modeling

`web corpora` · `instruction data` · `preference data` · `synthetic data` · `retrieval`

[Common Crawl](https://commoncrawl.org/) · [The Pile](https://github.com/EleutherAI/the-pile) · [FineWeb](https://huggingface.co/datasets/HuggingFaceFW/fineweb) · [Dolma](https://allenai.github.io/dolma/) · [The Stack](https://huggingface.co/datasets/bigcode/the-stack) · [FLAN](https://github.com/google-research/FLAN)

Training stack:

[PyTorch](https://pytorch.org/) · [Transformers](https://huggingface.co/docs/transformers/) · [FSDP](https://pytorch.org/docs/stable/fsdp.html) · [DeepSpeed](https://www.deepspeed.ai/) · [vLLM](https://docs.vllm.ai/) · [DataTrove](https://github.com/huggingface/datatrove)

---

## Systems

`Polars` · `PyArrow` · `DuckDB` · `Kafka` · `ClickHouse` · `Redis` · `PostgreSQL`

For reproducibility, the relevant object is not only the checkpoint:

```text
data snapshot
schema
feature definition
training split
model
evaluation config
```

For dependent data, validation follows the structure of the sample:

```text
temporal → split by time
longitudinal → split by entity
spatial → split by geography
language → remove duplicates / contamination
```
# Negative Results 

A collection of things that didn't work. 
- **Validation leakage was the most repeatable source of false confidence.** I ran into it in market time series, spatial tiles, repeated-patient data, and adjacent video frames. The correct split usually follows the dependence structure, not the row structure: [TimeSeriesSplit](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.TimeSeriesSplit.html), [GroupKFold](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GroupKFold.html), and explicit [spatial cross-validation](https://doi.org/10.1016/j.jag.2023.103364).

- **Some financial signals disappeared once I reconstructed information time correctly.** Observation date, publication date, ingestion date, and revision date are different variables; revised macro data was an especially clean example. [ALFRED vintage data](https://alfred.stlouisfed.org/help), [FRED vintage dates](https://fred.stlouisfed.org/docs/api/fred/series_vintagedates.html), and [SEC filing timestamps](https://www.sec.gov/edgar) make the distinction concrete.

- **Larger models did not consistently beat good low-capacity baselines.** On smaller text problems, [TF-IDF + logistic regression](https://scikit-learn.org/stable/auto_examples/text/plot_document_classification_20newsgroups.html) could stay surprisingly close to [BERT](https://arxiv.org/abs/1810.04805); on structured temporal data, linear / tree models such as [XGBoost](https://xgboost.readthedocs.io/) were often more stable than sequence models.

- **With video, detector quality and system quality were different problems.** [YOLO](https://github.com/ultralytics/ultralytics/blob/main/docs/en/modes/track.md) detections could be locally correct while occlusion, re-entry, or identity switches still corrupted counts over the full sequence. The failure was closer to [multi-object tracking](https://motchallenge.net/) and [ByteTrack](https://arxiv.org/abs/2110.06864) than to detector accuracy.

- **Interpolation made some sensor data easier to model for the wrong reason.** Regularizing asynchronous telemetry onto a clean grid could suppress abrupt changes, alter frequency content, and manufacture smooth local predictability. This showed up in standard [signal-processing](https://docs.scipy.org/doc/scipy/reference/signal.html) workflows and degradation settings such as [C-MAPSS](https://data.nasa.gov/dataset/C-MAPSS-Aircraft-Engine-Simulator-Data/xaut-bemq/about_data) from the [NASA Prognostics Data Repository](https://www.nasa.gov/intelligent-systems-division/discovery-and-systems-health/pcoe/pcoe-data-set-repository/).

- **Spatial CV was harsher than random CV.** Several remote-sensing / geospatial models looked strong until the test geography was genuinely separated from training. The model had partly learned location, acquisition conditions, or land-cover priors; [spatial cross-validation](https://doi.org/10.1016/j.jag.2023.103364), [BigEarthNet](https://bigearth.net/), and [SpaceNet](https://spacenet.ai/datasets/) are useful references for this failure mode.

- **Higher raster resolution did not mean higher information content.** Resampling could make a map look sharper while leaving the effective measurement support unchanged; this became important when joining [Landsat](https://www.usgs.gov/landsat-missions/landsat-collection-2), [Sentinel-2](https://sentinels.copernicus.eu/web/sentinel/missions/sentinel-2), [ERA5](https://www.ecmwf.int/en/forecasts/dataset/ecmwf-reanalysis-v5), point data, and administrative polygons.

- **Missingness sometimes carried more information than the imputed value.** This was clearest in clinical data: whether a test was ordered could itself encode physician assessment or patient state. Treating all missingness as a preprocessing defect removed part of the observation process; [MIMIC-IV](https://physionet.org/content/mimiciv/), [eICU](https://physionet.org/content/eicu-crd/), and [NHANES](https://www.cdc.gov/nchs/nhanes/) all make this structure visible.

- **Regularization stabilized nonparametric estimators but complicated inference.** In [kernel ridge regression](https://scikit-learn.org/stable/modules/kernel_ridge.html), RKHS / inverse-problem settings, stronger regularization could control variance while moving the target enough that naïve uncertainty statements became misleading. [Gaussian Processes](https://scikit-learn.org/stable/modules/gaussian_process.html) and constrained formulations in [CVXPY](https://www.cvxpy.org/) are useful comparisons because the structural assumptions are more explicit.

- **Pointwise success wasn't that good.** This mattered in [quantile regression](https://www.statsmodels.org/stable/generated/statsmodels.regression.quantile_regression.QuantReg.html) and functional work: an estimator could behave well at a selected index while becoming unstable across the full curve. The distinction becomes much more visible in [nonparametric estimation](https://www.statsmodels.org/stable/nonparametric.html) and regularized function estimation such as [kernel ridge](https://scikit-learn.org/stable/modules/kernel_ridge.html).

- **LLM data work produced larger gains than several model-side tweaks.** Deduplication, source quality, mixture composition, and label cleanup repeatedly mattered more than small architecture changes. [FineWeb](https://huggingface.co/datasets/HuggingFaceFW/fineweb), [Dolma](https://allenai.github.io/dolma/), and [DataTrove](https://github.com/huggingface/datatrove) are useful references because they treat corpus construction as part of the training problem.

- **Synthetic data saturated earlier than expected.** More examples stopped helping once the generator repeated the same style, reasoning pattern, or error distribution. The relevant questions became diversity, filtering, provenance, and rejection criteria rather than raw synthetic-token count; [FineWeb-Edu](https://huggingface.co/datasets/HuggingFaceFW/fineweb-edu), [OLMo](https://github.com/allenai/OLMo), and [Dolma](https://allenai.github.io/dolma/) are useful reference points.

- **RAG only helped when retrieval was the actual bottleneck.** If the model already had the relevant evidence and failed to reason over it, adding retrieval mostly added context. Likewise, more context could hurt when ranking / selection was weak. The distinction is clear in the original [RAG](https://arxiv.org/abs/2005.11401) formulation, [Lost in the Middle](https://arxiv.org/abs/2307.03172), and retrieval infrastructure such as [FAISS](https://github.com/facebookresearch/faiss).

- **Production failures were often data-contract failures, not model failures.** I have seen schema / distribution changes surface before service-health metrics moved; backfills also made supposedly reproducible offline runs disagree. [MLflow](https://mlflow.org/docs/latest/index.html), [Prometheus](https://prometheus.io/docs/), and [Apache Arrow](https://arrow.apache.org/docs/) are relevant here because model versioning without data lineage is not enough.
