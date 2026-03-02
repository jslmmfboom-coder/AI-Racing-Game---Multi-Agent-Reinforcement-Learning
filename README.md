# 🏎️ AI Racing Game - Multi-Agent Reinforcement Learning

一个基于深度强化学习（DQN）的多智能体赛车游戏，支持玩家与AI竞速。

![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## ✨ 特性

- 🤖 **多智能体强化学习**：3个AI赛车使用DQN算法进行训练
- 🎮 **玩家对战模式**：支持玩家与训练好的AI竞速
- 🗺️ **多样化赛道**：椭圆形（Oval）、花生形（Peanut）、肾形（Kidney）三种赛道
- 📊 **实时可视化**：使用Pygame实现游戏界面和排行榜
- 💾 **模型保存/加载**：支持训练进度保存和最佳模型加载
- 🏆 **积分系统**：完整的比赛积分和排名系统

## 🎯 游戏截图

### 游戏界面
- 绿色赛车：玩家控制
- 红色/橙色/紫色赛车：AI对手
- 黄色线：起点/终点线
- 灰色障碍物：需要避开
- 金色圆圈：加分道具

### 控制方式
- `↓` 或 `S`：恢复速度
- `←` 或 `A`：左转
- `→` 或 `D`：右转
- `ESC`：退出游戏

## 📦 安装

### 环境要求
- Python 3.8+
- PyTorch 2.0+
- Pygame 2.0+
- NumPy
- Matplotlib

### 安装步骤

1. 克隆仓库
```bash
git clone https://github.com/yourusername/ai-racing-game.git
cd ai-racing-game
```

2. 安装依赖
```bash
pip install -r requirements.txt
```

## 🚀 快速开始

### 1. 训练模式
训练AI模型（需要较长时间）：
```python
from main import main
main(mode='full_train')
```

训练参数：
- `num_episodes`: 600（训练轮数）
- `max_steps_per_episode`: 2000（每轮最大步数）
- `num_ai_cars`: 3（AI赛车数量）

### 2. 游玩模式
使用训练好的模型进行游戏：
```python
from main import main
main(mode='play')
```

### 3. 演示模式
快速测试游戏环境：
```python
from main import main
main(mode='demo')
```

## 🧠 技术架构

### DQN网络结构
```
输入层 (36维状态向量)
    ↓
全连接层 (256)
    ↓
全连接层 (128)
    ↓
全连接层 (64)
    ↓
输出层 (4个动作)
```

### 状态空间（36维）
- **自身状态** (7维)：位置、速度、方向、护盾、圈数进度
- **障碍物** (10维)：5个最近障碍物的距离和角度
- **对手** (15维)：5个最近对手的距离、角度、速度
- **道具** (4维)：4个最近道具的距离

### 动作空间（4个离散动作）
- 0: 无操作（保持当前速度）
- 1: 刹车
- 2: 左转
- 3: 右转

### 奖励函数
- ✅ 生存奖励：+0.3/步
- ✅ 速度奖励：基于当前速度
- ✅ 进度奖励：完成圈数进度 ×100
- ✅ 完成一圈：+1000
- ✅ 收集道具：+5
- ❌ 撞墙惩罚：-50
- ❌ 逆行惩罚：-5/步
- ❌ 死亡惩罚：-30

## 📁 项目结构

```
ai-racing-game/
├── Demo_1_1.ipynb          # Jupyter Notebook版本（完整代码）
├── main.py                 # 主程序入口
├── game_env.py            # 游戏环境和实体
├── dqn_agent.py           # DQN智能体实现
├── training.py            # 训练函数
├── visualization.py       # 可视化和UI
├── requirements.txt       # 依赖包列表
├── README.md             # 项目说明
├── LICENSE               # 开源协议
└── models/               # 训练好的模型
    ├── best_model_ep540_agent_0.pth
    ├── best_model_ep540_agent_1.pth
    └── best_model_ep540_agent_2.pth
```

## 🎓 算法说明

### DQN (Deep Q-Network)
本项目使用DQN算法训练AI赛车：

1. **经验回放**：存储和随机采样历史经验
2. **目标网络**：使用独立的目标网络稳定训练
3. **ε-贪婪策略**：平衡探索和利用
4. **多智能体训练**：3个AI同时训练，相互竞争

### 训练技巧
- 初始随机经验收集：1000步
- Epsilon衰减：0.990/轮
- 批量大小：128
- 学习率：0.001
- 折扣因子γ：0.95
- 目标网络更新频率：200步

## 📊 训练结果

经过600轮训练后：
- 平均奖励：6000+
- 完成率：AI能稳定完成3圈比赛
- 避障能力：显著提升
- 竞速策略：学会最优路线

## 🤝 贡献

欢迎提交Issue和Pull Request！

### 开发计划
- [ ] 添加更多赛道类型
- [ ] 实现多人在线对战
- [ ] 优化AI训练速度
- [ ] 添加回放系统
- [ ] 支持自定义赛道编辑器

## 📄 许可证

本项目采用 MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## 🙏 致谢

- PyTorch团队提供的深度学习框架
- Pygame社区的游戏开发支持
- 强化学习社区的算法参考

## 📧 联系方式

如有问题或建议，请通过以下方式联系：
- 提交Issue：[GitHub Issues](https://github.com/yourusername/ai-racing-game/issues)
- 邮箱：your.email@example.com

---

⭐ 如果这个项目对你有帮助，请给个Star！
