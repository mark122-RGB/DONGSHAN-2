# data/baselines/ — 话语层语域基线库

v2.0 引入。供 `scripts/discourse_profile.py --baseline` 做「特征-基线」比对：
Agent 第 3 步通读归因时，拿着偏离报告（deviations）定向读问题段落，不再盲扫全文。

## 文件

- `general.json` — 通用基线（当前唯一，48 篇真人实测，2026-08-12）

## 标定说明

- **来源**：`evals/corpus/` 48 篇真人语料实测重算（`scripts/baseline_manager.py --build`），
  非文献猜测。每个特征每个 register 组输出 P25 / P50 / P90 分位数。
- **register 分组**（按文件名前缀推断，非严格标注）：
  - `fiction`：essay_* / fic_*（散文/小说）
  - `keyzheng`：zhihu_*（知乎键政）
  - `general`：其余（net163_/sohu_/qq_/cnblogs/csdn/cctv/sina/feature/oral 等）
  - `all`：全部 48 篇
- **AI 对照**：`evals/corpus_ai/` 15 篇 AI 负样本仅用于区分度验证，不入库。
- **分位数口径**：P25/P50/P90 线性位置（`sorted(v)[int(len*0.25-1)]` 等）。

## 精度边界

- 基于简化中文处理（句首段正则 + 单点词性开关），不完整解析。
- 所有数值供定位参考，Agent 有否决权；已升引擎的指标（如 LW-PERSU-001 劝说性）
  在验收时需在基线范围内，偏离须给语域/文体理由。

## 重建

语料更新后重跑：`python scripts/baseline_manager.py --build`
