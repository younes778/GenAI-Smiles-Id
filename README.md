# 🧪 GenAI Chemical Evaluation Framework

## Overview
This repository contains a pipeline for benchmarking Generative AI models on chemical structure generation. Unlike standard metrics that only measure validity, this project implements a **stratified complexity assessment** and a **granular diagnosis engine**.

We aim to answer not just *if* a model fails, but *why* it fails (e.g., stereochemistry errors vs. hallucinations) and how these failures correlate with molecular complexity.

## 📊 Dataset & Stratification

We utilize the **[PharMolix/Vis-CheBI20](https://huggingface.co/datasets/PharMolix/Vis-CheBI20)** dataset as our ground truth.

### The Pipeline
1.  **Extraction:** We isolate SMILES strings from the source dataset.
2.  **Complexity Scoring:** We compute the **Synthetic Accessibility Score (`sa_score`)** for every molecule to quantify structural difficulty.
3.  **Binning & Sampling:**
    * Compounds are categorized into **Easy**, **Moderate**, and **Hard** tiers based on `sa_score`.
    * We generate a balanced evaluation set of **150 compounds** (50 per tier).

## 🧠 Diagnostic Methodology

We employ a custom evaluation algorithm (`get_smiles_metrics`) that moves beyond binary pass/fail checks. It uses **RDKit**, **Tanimoto Similarity**, and **InChI Layers** to classify predictions into specific error categories.

### Error Diagnosis Hierarchy

| Diagnosis Category | Description | Logic Used |
| :--- | :--- | :--- |
| **Perfect Match** | Prediction is identical to Ground Truth. | Canonical SMILES Match |
| **Stereochemistry Error** | Correct graph connectivity, wrong 3D orientation. | InChI Key Layer (Connectivity match, Stereo mismatch) |
| **Tautomer/Protonation** | Correct skeleton, wrong H-count/charge. | InChI Key Layer |
| **Constitutional Isomer** | Same atoms/formula, different connectivity. | Molecular Formula Match |
| **Fragment / Extra Atoms** | Prediction is a substructure (or superstructure) of Truth. | Substructure Match |
| **Scaffold Mismatch** | Prediction is chemically valid but structurally distinct. | Tanimoto Similarity < 0.4 |
| **Hallucination** | Output is not a valid chemical structure. | RDKit Parsing |

## 📈 Scoring
* **Validity:** Boolean check for chemical syntax.
* **Similarity:** Morgan Fingerprints (Radius 2, 2048 bits) with Tanimoto coefficient.

[Notebook](https://colab.research.google.com/drive/1ZnmmPhU5PPsADRccGiB674qY5GISpcAy?usp=sharing)
