# Reaction Optimization Tool

This project aims to develop a platform for predicting chemical reaction yields by combining molecular structure information, experimental conditions, and machine learning models. It focuses on building a data-driven approach to support chemists in optimizing reactions efficiently.

---

## Project Objectives


- **Data Collection, Cleaning, and Feature Engineering**

  Gather a reaction dataset with multiple type of reactions (e.g. coupling reactions, catalyzed transformations, classic organic reactions…)
  Extract relevant data such as SMILES of reactants/products/catalysts/solvents, temperature, reaction time, and yields.
  Use RDKit to convert SMILES into molecular descriptors (Morgan fingerprints, logP, molecular weight, etc.).  
  Apply one-hot encoding for categorical variables like solvents and catalysts.

- **Modeling**  

  Implement regression models first, followed by Neural Network modeling.
  Evaluate models using RMSE, R², and MAE metrics.

- **Visualization**  

  Analyze feature importance, cluster reactions by similarity, and compare model performances.

- **User Interface**

  Develop a Streamlit application to predict the yield of new reactions interactively.

---

## Current Status

Done:  
- **Project Structure** – Created folder architecture (data, src, notebooks, docs).  
- **Sample Dataset** – Added example reaction data (Buchwald-Hartwig Reaction) for initial testing.
- **Dataset Convertion** – Created a script to easily convert .pb databases into .csv files. 
- **Feature Extraction** – Developed RDKit-based scripts for molecular descriptor calculation.
- **Simple Models** – Construction and training of regression models (Random Forest, Linear Regression)

Ongoing:  
- **Proof of Concept** – Using Buchwald-Hartwig amination reaction data to validate the approach.
- **Data Collection Scripts** – Building scripts to gather and clean reaction datasets in bulk.  
- **Model Development** – Training initial machine learning models and tuning parameters.

Planned:
- **Advanced Visualizations** – Implement clustering and detailed feature analysis.
- **Expanded Dataset** – Incorporate other reaction types and experimental conditions.
- **User Interface** – Build a web app for yield prediction using Streamlit.  

---

Informations about installation and use of the repo will be provided as the project progresses.
