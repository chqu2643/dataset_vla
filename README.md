# dataset_vla

三个常用开源具身 VLA 仿真 benchmark 的固定快照，全部保持官方
[LeRobot](https://github.com/huggingface/lerobot) v3.0 目录格式。

快照日期：2026-10-13。选择时以 Hugging Face 官方 `lerobot` 组织中的下载量作为可复现的使用热度指标，并要求来自三个不同的仿真 benchmark 系列。

| Benchmark | 上游数据集 | Episodes | Tasks | 快照大小（十进制） | 选取时下载量 | License |
|---|---|---:|---:|---:|---:|---|
| PushT | [`lerobot/pusht`](https://huggingface.co/datasets/lerobot/pusht) | 206 | 1 | 7.69 MB | 27,847 | MIT |
| ALOHA Sim Transfer Cube (Human) | [`lerobot/aloha_sim_transfer_cube_human`](https://huggingface.co/datasets/lerobot/aloha_sim_transfer_cube_human) | 50 | 1 | 69.88 MB | 48,659 | MIT |
| LIBERO | [`lerobot/libero`](https://huggingface.co/datasets/lerobot/libero) | 1,693 | 40 | 1.94 GB | 18,529 | Apache-2.0 |
| **合计** |  | **1,949** | **42** | **2.013 GB** |  |  |

每个数据集均小于 3 GB，合计小于 9 GB。精确字节数、上游 commit 和更新时间见 [`SOURCES.json`](SOURCES.json)。

## 获取数据

仓库中的 Parquet 和 MP4 文件使用 Git LFS：

```bash
git lfs install
git clone https://github.com/chqu2643/dataset_vla.git
cd dataset_vla
sha256sum -c SHA256SUMS
```

如果已经普通克隆但只有 LFS 指针，请运行：

```bash
git lfs pull
```

## 用 LeRobot 从本地读取

安装与数据版本相容的 LeRobot 后，可以给 `LeRobotDataset` 传入本地根目录：

```python
from pathlib import Path
from lerobot.datasets.lerobot_dataset import LeRobotDataset

repo_root = Path.cwd()
pusht = LeRobotDataset(
    repo_id="lerobot/pusht",
    root=repo_root / "datasets" / "pusht",
)
aloha = LeRobotDataset(
    repo_id="lerobot/aloha_sim_transfer_cube_human",
    root=repo_root / "datasets" / "aloha_sim_transfer_cube_human",
)
libero = LeRobotDataset(
    repo_id="lerobot/libero",
    root=repo_root / "datasets" / "libero",
)
```

数据目录没有改名或转换；每个目录中的 `meta/info.json`、Parquet 分片和 MP4 分片均来自表中固定的上游 commit。

## 选择说明

- PushT：广泛用于视觉操作策略的轻量仿真基准。
- ALOHA Sim Transfer Cube：经典双臂协同操作仿真任务；这里采用 human demonstrations 版本。
- LIBERO：面向语言条件、多任务和持续学习的仿真操作 benchmark，本快照包含 40 个任务。

“常用”不是一个永久排名；这里使用 2026-10-13 记录的 Hugging Face 下载量作近似指标，同时优先保证 benchmark 多样性，而不是从同一 ALOHA 系列重复选取多个任务。

## 来源与许可

数据版权与许可仍归各上游项目所有。本仓库不对三个数据集重新授权：PushT 和 ALOHA 数据卡标注 MIT，LIBERO 数据卡标注 Apache-2.0。使用前请阅读各数据集目录内保留的原始 `README.md` 和上游项目条款。
