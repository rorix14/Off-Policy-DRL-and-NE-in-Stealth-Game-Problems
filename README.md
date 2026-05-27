# Comparing the Performance of Off-Policy Deep Reinforcement Learning and Neuroevolution in Stealth Game Problems

**Authors:** Pedro F. Silva¹, Jacinto Estima¹, Inês Nobre², Edirlei Soares de Lima³

¹ Department of Informatics Engineering, CISUC/LASI, University of Coimbra, 3004-531 Coimbra, Portugal  
² CIPER, Faculty of Human Kinetics, University of Lisbon, 1499-002 Oeiras, Portugal  
³ Academy for AI, Games and Media, Breda University of Applied Sciences, 4817 JS Breda, Netherlands

**Corresponding author:** Pedro F. Silva (pedrosilva333@outlook.pt)

---

## Abstract

This repository contains the Unity project developed for the paper *"Comparing the Performance of Off-Policy Deep Reinforcement Learning and Neuroevolution in Stealth Game Problems"*.

The project implements and evaluates eighteen Deep Learning algorithms — eight off-policy Deep Reinforcement Learning (DRL) variants of DQN and ten Neuroevolution (NE) algorithms — across three custom stealth game environments built in Unity. 

> **Citation:** [Paper DOI placeholder — to be updated upon publication]  
> **Archived repository:** [![DOI](https://zenodo.org/badge/1251660042.svg)](https://doi.org/10.5281/zenodo.20418839)

---

## Requirements

- **Unity version:** 2020.3.37f1 LTS
- **Unity packages:**
  - `Jobs` — used for parallel execution of NE population evaluations; this is the most critical package dependency and must be installed for the project to run correctly

---

## Repository Structure

The relevant content of the project lives under the `Assets/` folder:

```
Assets/
│
├── Comparing the Performance of Off-Policy Deep Reinforcement Learning
│   and Neuroevolution in Stealth Game Problems/
│   │   # Contains all algorithm prefabs with their best-found hyperparameter
│   │   # configurations, as reported in the paper. Organized by level and
│   │   # algorithm family.
│   │
│   ├── Level_1/
│   │   ├── DRL/    # DRL algorithm prefabs tuned for Level 1
│   │   └── NE/     # NE algorithm prefabs tuned for Level 1
│   │
│   ├── Level_2/
│   │   ├── DRL/    # DRL algorithm prefabs tuned for Level 2
│   │   └── NE/     # NE algorithm prefabs tuned for Level 2
│   │
│   └── Level_3/
│       ├── DRL/    # DRL algorithm prefabs tuned for Level 3
│       └── NE/     # NE algorithm prefabs tuned for Level 3
│
├── Scenes/
│   ├── Level_1    # Corresponds to level one (a) in the paper
│   ├── Level_2    # Corresponds to level two (b) in the paper
│   └── Level_3    # Corresponds to level three (c) in the paper
│
├── Scripts/
│   │   # All C# scripts implementing the DRL and NE algorithms,
│   │   # environment logic, and training infrastructure.
│   └── ...
│
└── Test Data/
    └── Preliminary algorithm Tests/
            # Training results are saved here when data saving is enabled
            # (see "Saving Training Data" section below)
```

---

## Replicating the Results

### 1. Open a Scene

Open one of the three scenes in `Assets/Scenes/`:

| Scene name | Corresponds to |
|---|---|
| `Level_1` | Level one (a) in the paper |
| `Level_2` | Level two (b) in the paper |
| `Level_3` | Level three (c) in the paper |

### 2. Enable the Desired Algorithm Group

In the Unity **Hierarchy** panel, each scene contains two GameObjects:

- **`Test DQN algorithms`** — runs all DRL (DQN-based) algorithms sequentially
- **`Test NE algorithms`** — runs all NE algorithms sequentially

Both objects are **disabled by default**. To run a group, select it in the Hierarchy and enable it in the Inspector. 

> ⚠️ Do not enable both objects at the same time. Run DRL and NE experiments separately.

Each object holds an ordered list of algorithm prefabs (sourced from the `Comparing the Performance...` folder described above). Algorithms are trained sequentially in list order. The list ordering can be changed in the Inspector if you wish to run a subset or reorder experiments.

### 3. Random Seeds

Random seeds are generated automatically by the `Test DQN algorithms` and `Test NE algorithms` objects. They reproduce the exact same ten seeds used to produce the results reported in the paper. No manual seed configuration is needed.

### 4. Run the Scene

Press **Play** in the Unity Editor. Training will begin automatically for the first algorithm in the list and proceed sequentially through all algorithms in the group.

---

## Saving Training Data

Both `Test DQN algorithms` and `Test NE algorithms` expose the following variables in the Inspector:

| Variable | Type | Default | Description |
|---|---|---|---|
| `Save Data` | `bool` | `false` | When `true`, training metrics are saved to disk after each algorithm finishes |
| `Save File Name` | `string` | *(user-defined)* | The name of the output file |

When saving is enabled, output files are written to:

```
Assets/Test Data/Preliminary algorithm Tests/
```

Set `Save Data` to `true` and provide a `Save File Name` before pressing Play if you wish to record results.

---

## Algorithms Implemented

### Off-Policy DRL (DQN variants)
- DQN
- Double DQN
- Dueling DQN
- N-step DQN
- DQN with Prioritized Experience Replay (PER)
- Noisy DQN
- Categorical DQN (C-51)
- Rainbow DQN

### Neuroevolution
- Random Search (RS)
- Covariance Matrix Adaptation Evolutionary Strategy (CMA-ES)
- Genetic Algorithm (GA)
- Neuroevolution of Augmenting Topologies (NEAT)
- RS with Novelty Search (RS-NS)
- CMA-ES with Novelty Search (CMA-ES-NS)
- GA with Novelty Search (GA-NS)
- NEAT with Novelty Search (NEAT-NS)

---

## Hardware Used

All experiments reported in the paper were conducted on:

- CPU: AMD Ryzen 9 7900X
- GPU: NVIDIA GeForce RTX 3070
- RAM: 32 GB
