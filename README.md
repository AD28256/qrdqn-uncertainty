# qrdqn-uncertainty

Coursework project for BIOE70077 Reinforcement Learning for Bioengineers (Imperial College London, 2026–27).

**Topic (working title):** Can the return distribution learned by QR-DQN act as a reliability signal for the agent's behaviour?
The research question will be refined in the project plan.

## Source method and code

**Method (source paper)**
Dabney, W., Rowland, M., Bellemare, M. G., & Munos, R. (2018). *Distributional Reinforcement Learning with Quantile Regression.* Proceedings of the AAAI Conference on Artificial Intelligence, 32(1). arXiv:1710.10044.

The authors did not release an official implementation, so this project uses a widely used, actively maintained implementation:

| Component | Repository | Version used | Licence |
|---|---|---|---|
| QR-DQN implementation | [Stable-Baselines-Team/stable-baselines3-contrib](https://github.com/Stable-Baselines-Team/stable-baselines3-contrib) | v2.9.2 | MIT |
| Core library | [DLR-RM/stable-baselines3](https://github.com/DLR-RM/stable-baselines3) | v2.9.2 | MIT |
| Training framework and tuned hyperparameters | [DLR-RM/rl-baselines3-zoo](https://github.com/DLR-RM/rl-baselines3-zoo) | v2.9.2 | MIT |

All packages were installed from PyPI at the versions above; the full environment is pinned in `requirements.txt`.

**Implementation citations**
- Raffin, A., Hill, A., Gleave, A., Kanervisto, A., Ernestus, M., & Dormann, N. (2021). Stable-Baselines3: Reliable Reinforcement Learning Implementations. *Journal of Machine Learning Research*, 22(268), 1–8.
- Raffin, A. (2020). RL Baselines3 Zoo. GitHub repository. https://github.com/DLR-RM/rl-baselines3-zoo

**Backup candidate:** C51 (Bellemare, Dabney & Munos, ICML 2017) via [CleanRL](https://github.com/vwxyzjn/cleanrl) (MIT).

## Setup (Windows, Anaconda)

```
conda create -n rlcw python=3.10 -y
conda activate rlcw
python -m pip install -r requirements.txt
```

**Known issue:** `rl_zoo3` 2.9.2 does not install `requests`, which `rl_zoo3.enjoy` needs. It is included in `requirements.txt`; if installing `rl_zoo3` on its own, run `python -m pip install requests` as well.

## Smallest example (environment check)

Train QR-DQN on CartPole-v1 with RL Zoo's tuned hyperparameters (50k steps), then evaluate:

```
python -m rl_zoo3.train --algo qrdqn --env CartPole-v1 --seed 0 -f logs
python -m rl_zoo3.enjoy --algo qrdqn --env CartPole-v1 -f logs --no-render -n 5000
```

| | Result |
|---|---|
| This run (seed 0, 10 evaluation episodes) | 500.00 ± 0.00 |
| Reference (RL Zoo `benchmark.md`, QR-DQN, CartPole-v1, 50k steps) | 500.00 ± 0.00 |

This confirms the environment works. It is not the baseline reproduction, which will use multiple seeds and the reference evaluation protocol.

## Licence

MIT (see `LICENSE`).
