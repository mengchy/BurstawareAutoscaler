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
- Grafana K6
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
3. Deploy the benchmark application to Kubernetes:
   ```bash
   kubectl apply -f ./app/app.yaml
   ```

## Usage
### Running BASE on Kubernetes：
1. Start workload sending backend:
   ```bash
   bash ./k6/background.sh
   ```
2. Modify `config.json` to configure experiment settings：
    ```json
   {
    "k6_server_addr": ["10.186.117.4:6565","10.186.117.5:6565","10.186.117.7:6565","10.186.117.8:6565"],
    "prometheus_addr": "127.0.0.1:30090",
    "prometheus_query_interval": "1m",
     ...
    "method": "onestep",
    "cur_mode": "vali",
    "time_interval": 120, 
    "interval_start": 1000,
    "interval_length": 720,
    "hyperparameter":[{
        "workload_name": "2018_FIFA_World_Cup",
        "start_point": 30,
        "train_step": 6000,
        "vali_step": 2000,
        "test_step": 2000,
        "des_mean": 500,
        "des_std": 175,
        "sla": 16,
        "action_max": 10}]
    }
   ```
4. Launch BASE autoscaler:
   ```bash
   python main.py --config_filename config.json
   ```
### Running BASE on Simulation：
1. Go to the simulation directory:
   ```bash
   cd ./simulator
   ```
2. Modify `main.json` to set workload parameters, SLO thresholds, and scaling policies:
   ```python
   aim_csv_file = "validate_output.csv" # Output flie
   sla=16   # SLO thresholds
   data_list = ["2018_FIFA_World_Cup","Barack_Obama","Donald_Trump","Elizabeth_II","Elon_Musk","Facebook","Game_of_Thrones","Google","United_States","YouTube"]
   reward_ratio_change_list = [0.1]
   ...
   # Choose scaling policies
   choose_use_ppo = True                      # BASE
   choose_use_burst_aware_prediction = False  # BAPA
   choose_use_asarsa = False                   # A-SARSA
   choose_use_onestep_prediction = False      # ShortPred
   choose_use_multistep_prediction = False      # LongPred
   choose_use_reactive_threshold = False       # K8S-HPA
   ```
3. Launch BASE autoscaler:
   ```bash
   python main.py
   ```
   
## Experiments
BASE has been validated using real-world workloads from the Wikimedia dataset, including Google, YouTube, Facebook, and more. Experimental results demonstrate superior performance in reducing SLO violations while maintaining cost efficiency.

## Citation
If you use BASE in your research, please cite our paper:
```bibtex
@article{BASE2025,
  title={Burst-Aware Autoscaling via Stacked Ensembles: Balancing SLO Assurance and Cost Efficiency},
  author={XXX et al.},
  journal={ICWS},
  year={2025}
}
```

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributors
- XXX (@your-github)
- Collaborators (@collaborator-github)

## Acknowledgments
We thank the open-source community for providing the tools and datasets that made this research possible.

## Contact
For questions or collaboration, please open an issue or contact `XXX@example.com`.
