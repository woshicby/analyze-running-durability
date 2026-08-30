# 跑者耐久性分析

[English README](README.md)

这是一个用于分析跑者在多次长距离训练中保持输出能力的 OpenAI 技能。它综合心率—输出解耦、RPE、补给、天气、地形、症状出现顺序以及训练后 24–48 小时恢复情况，判断当前最可能的限制因素，并设计下一步最有区分度的训练实验。

## 功能

- 设计四周耐久性现场测试，安排三次具有可比性的长距离训练。
- 统一计算速度或跑步功率效率、碳水和液体摄入、RPE 变化与首次变化时间。
- 先判断训练之间是否可比，再解释趋势。
- 明确区分观测数据、可能解释、竞争性解释、结论置信度和下一项区分性测试。
- 适用于公路跑、越野跑、马拉松和超长距离场景，不把单次解耦率当作诊断或通用合格线。
- 输出简洁的教练报告，并识别应停止运动表现分析、建议就医评估的症状。

## 目录结构

```text
analyze-running-durability/
├── SKILL.md
├── agents/openai.yaml
├── assets/icon.svg
├── references/
│   ├── data-schema.md
│   └── interpretation.md
└── scripts/summarize_durability.py
```

`SKILL.md` 是技能入口；两份参考文档分别定义数据结构和解释框架；Python 脚本只负责确定性的 CSV 归一化计算，不会自动诊断或决定训练方案。

## 安装

### ChatGPT

将本仓库下载为 ZIP，通过 ChatGPT 的“技能”界面导入技能文件夹，并保持原有目录结构。

### Codex

把仓库克隆到本地技能目录：

```bash
git clone https://github.com/SrJackCM/analyze-running-durability.git \
  ~/.codex/skills/analyze-running-durability
```

如果 Codex 没有立即发现技能，请重启或刷新 Codex。

## 使用方法

显式调用技能：

```text
使用 $analyze-running-durability 比较我最近四次长距离训练，判断最先下降的环节，并给出下一阶段四周训练重点。
```

建议提供：训练时长，上下半程心率及速度或功率，RPE，碳水与液体摄入，天气，路线和爬升，最先出现的变化及其时间，以及 24 小时和 48 小时恢复情况。缺失数据应明确标注，不应虚构。

### CSV 辅助脚本

脚本只使用 Python 标准库，需要 Python 3.9 或更高版本。

```bash
python3 scripts/summarize_durability.py long-runs.csv > summary.md
```

使用 `--metric speed` 或 `--metric power` 可强制指定输出指标。支持的字段见[数据结构说明](references/data-schema.md)。

## 解释与安全边界

- 解耦率只是心率—输出关系的一项摘要，不是完整的耐久性评分。
- 路线、天气、海拔、停顿、传感器质量、配速、补给、疾病、疼痛和恢复状态都可能影响解释。
- 本技能用于运动表现分析和教练决策支持，不用于医疗诊断。
- 出现胸痛、晕厥、神经系统症状、异常严重的呼吸困难、伴随严重肌肉疼痛的深色尿、消化道出血、持续无法摄入液体、急性损伤、改变步态的疼痛，或训练外持续加重的症状时，应停止表现分析并寻求适当的临床评估。

## 参与贡献

欢迎提交 Issue 和范围明确的 Pull Request。请保留以证据链为核心的解释方式，避免在缺乏充分依据时加入通用的合格或不合格阈值。
