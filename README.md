# Astronomy-X-Machine-Learning-Research-Project
Introduction: 

The discovery of exoplanets has revolutionized modern astronomy. Since the first discovery of an exoplanet in the 1990s, thousands of exoplanets have been discovered. Some of these exoplanets are located at close proximity to their respective stars. Others are found at greater distances from their respective stars. On the other hand, the discovery of exoplanets is of interest due to the possibility of the existence of life. The search for other habitable planets is the main reason that makes the discovery of exoplanets important. 

 Generally, habitability refers to the potential that a planet contains to have liquid water on the surface; and indeed, water is a fundamental component to have on a planet if one is looking for life. Yet, the measurement of the habitability of a planet is quite difficult. Indeed, the number of measurements that have been made on the various parameters of the atmosphere of the detected exoplanets is not large. Yet, certain parameters can be observed on the outside that might suggest habitability. 

Several schemes have been developed to quantify these parameters, collectively know as habitability metrics or HMs. Among those schemes are Earth Similarity Index-like techniques and others based on parameter scoring functions. Generally, these employ radius or mass of planets, equilibrium temperatures, and characteristics of their host stars to estimate the possibility that a given exoplanet might reside within a (possibly several) habitable zones. However, these approaches also have limitations: they tend to be based on certain thresholds or simplistic formulations. In addition, there is a nascent potential to employ some recent statistical and machine learning techniques to study trends within exoplanet data sets. 

Machine learning has been increasingly applied to various tasks within astronomy, including exoplanet detection, classification, and parameter estimation. When machine learning is applied to the habitability of exoplanets, however, it is important to do so with care. This is due to the fact that habitability does not represent a well-separated class within parameter space, and because datasets are always imbalanced, with only a small percentage being considered potentially temperate and Earth-like. 

For this manuscript, we discuss a data-driven model to calculate relative exoplanet habitability using existing data on exoplanets and stars. The Exoplanet Archive provided by NASA and data from the Planetary Habitability Laboratory are used to create a dataset containing confirmed exoplanets with known properties. The habitability score is defined based on equilibrium temperature, radius, mass, as well as star properties. Various models are tested in this regard, considering the class imbalance problem. 

Rather than attempting to claim confirmation of habitable worlds, this study aims to provide a systematic ranking framework that may assist in identifying promising candidates for further observational follow-up. By combining physics-based reasoning with modern data analysis techniques, this work seeks to contribute to ongoing efforts in understanding planetary environments beyond our Solar System. 

 

Data Sources and Pre-Processing 

This study is based on publicly available exoplanet data obtained from two primary sources: the NASA Exoplanet Archive and the Planetary Habitability Laboratory (PHL) catalog. The NASA archive provides detailed planetary and stellar measurements derived from observational surveys, including planetary radius, planetary mass, orbital period, equilibrium temperature, stellar effective temperature, stellar mass, and stellar radius. The PHL catalog was used to complement this dataset and cross-check planetary information. 

The two datasets were merged using planetary identifiers to ensure that records corresponded to the same confirmed exoplanets. Only planets with available measurements for the key physical and stellar parameters were retained. The selected features—planetary radius, planetary mass, equilibrium temperature, orbital period, stellar effective temperature, stellar mass, and stellar radius—were chosen because they are directly observable quantities that are commonly associated with potential surface habitability. 

During preprocessing, duplicate entries were removed and planets with missing essential measurements were excluded to maintain consistency. Continuous variables were inspected to ensure physically reasonable ranges. Skewed distributions, particularly in planetary mass and orbital period, were preserved rather than artificially truncated, as they reflect known observational biases in exoplanet detection methods. 

For modeling purposes, features were standardized to ensure that variables operating on different numerical scales contributed comparably during training. Standardization was performed after splitting the dataset to prevent information leakage between training and evaluation sets. Where necessary, non-critical missing values were handled using standard imputation techniques. 

The final dataset consists of confirmed exoplanets with complete measurements for the selected parameters. When habitability criteria are applied, the dataset exhibits strong class imbalance, as only a small fraction of known planets fall within temperate and Earth-sized regimes. This imbalance was preserved to reflect the true distribution of currently known exoplanets and was addressed explicitly during model evaluation rather than artificially corrected. 

Overall, the preprocessing pipeline was designed to maintain physical realism while preparing the dataset for systematic statistical analysis. The objective was not to curate a subset of “likely habitable” planets in advance, but to analyze the full available population in a consistent and reproducible manner.

Physical Interpretation of Model Behavior
To check that the model was not only statistically accurate but also physically meaningful, we
examined how the predicted habitability score relates to key planetary parameters. The scatter
plot of habitability score versus equilibrium temperature shows that higher scores are mostly
concentrated between about 250–320 K, which represents temperate conditions. Planets with
extremely high temperatures (above 1000 K) or very low temperatures receive near-zero scores.
This suggests that the model correctly penalizes extreme thermal environments.
A similar pattern appears when comparing habitability score with planetary radius. The highest
scores occur near one Earth radius, while very large planets, likely gas giants, receive very low
scores. This shows that the model favors rocky, Earth-sized planets over gaseous ones. Overall,
these results indicate that the model captures physically meaningful patterns rather than random
statistical relationships.

Top 20 Candidate Planets
After training the final XGBoost model on the full dataset, habitability scores were computed for
all planets. The top 20 planets with the highest predicted scores were selected for further
analysis.
Notably, the list includes several well-known and scientifically credible candidates, such as:
• Teegarden’s Star b
• Ross 128 b
• Proxima Centauri d
• TRAPPIST-1 d
• TRAPPIST-1 e
• Kepler-1649 b
• Kepler-445 d
These planets are already discussed in the scientific community as potentially temperate or rocky
worlds, which increases confidence in the model’s ranking.
Statistical analysis of the Top 20 planets reveals:
• Equilibrium temperatures mostly between 250–320 K
• Planetary radii clustered around ~1 Earth radius
• Host stars with moderate effective temperatures

Cross Validation and Model Behaviour

To check whether the model is reliable, five-fold cross-validation was performed. The dataset
was divided into five parts, and the model was trained and tested five times using different splits.
The R² boxplot shows that performance remains high in all folds. The RMSE boxplot shows that
prediction errors are small and stable.
This means the model is not overfitting one specific data split. It performs consistently across
different subsets of the data and generalizes well within the observed exoplanet sample.
