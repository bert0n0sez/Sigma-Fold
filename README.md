# Sigma-Fold
A neural network project. Prediction of the secondary structure of a protein by its amino acid sequence.

Creators: Albert V. I., Denis A. G., Andrey A. H.

## Overview

This project implements a transformer model for protein secondary structure prediction, treating it as a sequence labeling task similar to Named Entity Recognition (NER) in Natural Language Processing. The model predicts structural labels (H, E, C) for each amino acid in a protein sequence.

**Key Features:**
- Transformer architecture implementation from scratch
- Pre-trained ESM embeddings for protein sequences
- Multi-class classification for secondary structure elements
- Evaluation using Q3 score (3-state accuracy)

## Problem Description

Protein secondary structure prediction involves classifying each amino acid in a protein sequence into one of three structural classes:
- **H** (Helix/α-helix)
- **E** (Sheet/β-strand) 
- **C** (Loop/Coil)

This is a fundamental problem in bioinformatics with applications in protein function analysis and 3D structure prediction.

## Dataset

The model is trained and evaluated on standard protein structure datasets:
- **CASP** (Critical Assessment of Structure Prediction)
- **CB513** (Curated benchmark dataset)

### Data Format
- Input: Amino acid sequences (strings of 20 standard residues)
- Output: Sequence of secondary structure labels (H, E, C)
- Example: `"MSEV"` → `"HECC"`

## Model Architecture
