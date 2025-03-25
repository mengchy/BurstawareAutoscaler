# BASE: Burst-aware Autoscaling via Stacked Ensembles

**NOTE:** Documentation is being progressively improved!

## Introduction
BASE is a machine-learning-based autoscaling framework for containerized cloud services and applications. It leverages a stacked ensemble of models to mitigate Service-Level Objective (SLO) violations while minimizing resource costs under dynamic workloads. BASE features a novel burst detection mechanism to distinguish between predictable workload peaks and actual bursts, ensuring efficient and adaptive resource allocation.

## Features
- **Burst Detection and Handling:** Introduces a prediction-based mechanism to differentiate between periodic workload spikes and true bursts, overestimating and allocating resources to manage rapid demand growth.
- **Estimation Enhancement:** Leverages reinforcement learning to improve resource estimation accuracy, enabling more precise resource allocation during stable periods.
- **Burst-Aware Autoscaling:** Develops a targeted autoscaling framework that adapts resource planning based on workload characteristics, optimizing service level objectives (SLO) and cost efficiency.

## Installation
### Prerequisites
- Kubernetes (v1.23+)
- Istio (v1.14+)
- Python (>=3.8)
- Docker
- Prometheus & Grafana for monitoring

### Setup Instructions
1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/BASE.git
   cd BASE
   ```
2. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Deploy to Kubernetes:
   ```bash
   kubectl apply -f deployment.yaml
   ```

## Usage
### Running BASE
1. Start monitoring services:
   ```bash
   ./scripts/start_monitoring.sh
   ```
2. Launch BASE autoscaler:
   ```bash
   python main.py --config config.yaml
   ```

### Configuration
Modify `config.yaml` to set workload parameters, SLO thresholds, and scaling policies.

## Experiments
BASE has been validated using real-world workloads from the Wikimedia dataset, including Google, YouTube, Facebook, and more. Experimental results demonstrate superior performance in reducing SLO violations while maintaining cost efficiency.

## Citation
If you use BASE in your research, please cite our paper:
```bibtex
@article{BASE2025,
  title={Burst-Aware Autoscaling via Stacked Ensembles: Balancing SLO Assurance and Cost Efficiency},
  author={Your Name et al.},
  journal={IEEE ICWS},
  year={2025}
}
```

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributors
- Your Name (@your-github)
- Collaborators (@collaborator-github)

## Acknowledgments
We thank the open-source community for providing the tools and datasets that made this research possible.

## Contact
For questions or collaboration, please open an issue or contact `your-email@example.com`.
