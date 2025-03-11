# BASE: A Burst-aware Autoscaler via Stacked Ensembles

This is the origin python implementation of BASE in the following paper: `Burst-Aware Autoscaling via Stacked Ensembles: Balancing SLO Assurance and Cost Efficiency`. 

**Note: We are refining the REDME documentation.**

## Require

```
python  3.6.0
torch  1.8.2
gym  0.22
pandas  1.4
numpy  1.22
sklearn  1.2
```

## Running

### Load generate using k8

```bash
cd k6
bash background.sh 
```

### Autoscaling on Kubernetes

```bash
python -u main.py
```

### Autoscaling on Simulation

```bash
cd simulation
python -u main.py
```
