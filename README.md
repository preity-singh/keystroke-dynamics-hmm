# Keystroke HMM Authentication

Behavioral authentication using **keystroke timing** from a fixed password.  
We discretize timing features and train a **discrete HMM per user**, then identify the most likely user by log-likelihood.

## Data
- Keystroke Dynamics Benchmark (CMU CyLab), `DSL-StrongPasswordData.csv`
- Each row = one repetition of the same password by a subject
- Features include hold times (H.*) and latencies (DD.*, UD.*)

## Approach
1. **Preprocess**: take the 31 timing features and **discretize** them into `m` bins (quantile-based).
2. **Train**: one **discrete HMM per user** with Baum–Welch (EM).
3. **Predict**: for a new sequence, compute log-likelihood under every user’s HMM and choose the max.

## Notes
- Discrete HMM requires discretization of continuous timing values.
- Results depend on hyperparameters like number of bins `m` and number of hidden states.
