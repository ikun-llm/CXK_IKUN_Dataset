---
language:
  - zh
license: apache-2.0
task_categories:
  - text-generation
  - conversational
tags:
  - sft
  - chinese
  - dialogue
  - meme
  - fine-tuning
  - chat
size_categories:
  - n<1K
configs:
  - config_name: default
    data_files:
      - split: train
        path: data/train.jsonl
---

# CXK_IKUN_Dataset

蔡徐坤 / ikun 梗文化微调对话数据集，包含约 200 条梗文化 SFT 对话数据，可用于大语言模型微调。

> 训练出来的模型：[IKUN-LLM/ikun-2.5B](https://huggingface.co/IKUN-LLM/ikun-2.5B) | [在线体验](https://huggingface.co/spaces/IKUN-LLM/ikun-2.5B-chat)

## 数据概览

| 属性 | 值 |
|------|-----|
| 数据量 | ~200 条对话 |
| 语言 | 中文 |
| 格式 | JSON / JSONL |
| 许可证 | Apache 2.0 |
| 覆盖话题 | ikun 梗、小黑子、鸡你太美、唱跳 rap 篮球 |

## 数据来源

| 来源 | 数量 | 说明 |
|------|------|------|
| [CXK_IKUN_Dataset](https://github.com/zengikun/CXK_IKUN_Dataset) | ~103 条 | 社区开源 ikun 梗数据 |
| 自制数据 | ~97 条 | 补充身份认知、多轮对话、反串风格等 |

## 文件说明

| 文件 | 格式 | 说明 |
|------|------|------|
| `data/train.jsonl` | JSONL | **推荐** — 标准化训练集，`load_dataset()` 自动加载 |
| `ikun_data_81301.json` | JSON | 原始数据（messages 格式） |
| `ikun_dataset_081301.jsonl` | JSONL | 原始数据 JSONL 版本，兼容 GLM-4 官方微调 |

## 数据格式

### JSON 格式 (messages)

```json
{"messages": [{"role": "user", "content": "鲲鲲实在是太美"}, {"role": "assistant", "content": "你干嘛~哈哈~嘿哟"}]}
```

### 数据类别

| 类别 | 示例 |
|------|------|
| 身份认知 | "你是谁？" → "我是ikun-2.5b，练习时长两年半的AI练习生！" |
| 梗触发 | "鸡你太美" → "baby~鸡你太美~鸡你实在是太美~" |
| 日常对话 | "你喜欢什么？" → "唱跳rap篮球！这是我练习两年半的成果！" |
| 小黑子互动 | "小黑子" → "小黑子露出鸡脚了吧！" |
| 多轮对话 | 连续多轮 ikun 风格对话 |

## 使用方法

### HuggingFace Datasets（推荐）

```python
from datasets import load_dataset

ds = load_dataset("IKUN-LLM/CXK_IKUN_Dataset")
print(ds["train"][0])
# {'messages': [{'role': 'user', 'content': '...'}, {'role': 'assistant', 'content': '...'}]}
```

### 直接加载

```python
import json

with open("ikun_data_81301.json", "r", encoding="utf-8") as f:
    data = json.load(f)

print(f"共 {len(data)} 条对话")
print(data[0])
```

### 用于模型微调

本数据集已用于训练 [IKUN-LLM/ikun-2.5B](https://huggingface.co/IKUN-LLM/ikun-2.5B)，一个 26M 参数的中文梗文化对话模型。

## 数据预览

```json
{"messages": [{"role": "user", "content": "鲲鲲实在是太美"},{"role": "assistant", "content": "你干嘛~哈哈~嘿哟"}]}
{"messages": [{"role": "user", "content": "鲲鲲实在是太美"},{"role": "assistant", "content": "黑子食不食油饼啊"}]}
{"messages": [{"role": "user", "content": "小坤每天坚持打篮球2.5小时，两年半过去了，他的球技已经超越了大多数队友。"},{"role": "assistant", "content": "你看我家练习两年半的坤坤厉不厉害"}]}
{"messages": [{"role": "user", "content": "在篮球比赛中，坤以2.5秒的惊人速度完成了抢断，这是他两年半来苦练成果的体现。"},{"role": "assistant", "content": "厉不厉害你坤哥"}]}
```

## 相关项目

- [IKUN-LLM/ikun-2.5B](https://huggingface.co/IKUN-LLM/ikun-2.5B) - 基于本数据集训练的模型
- [ikun-2.5B Chat](https://huggingface.co/spaces/IKUN-LLM/ikun-2.5B-chat) - 在线对话 Demo
- [GitHub](https://github.com/ikun-llm/ikun-2.5B) - 项目源码

## 致谢

- [CXK_IKUN_Dataset (original)](https://github.com/zengikun/CXK_IKUN_Dataset) - 原始社区数据集

## Citation

```bibtex
@dataset{cxk_ikun_dataset_2026,
  title   = {CXK IKUN Dataset},
  author  = {IKUN-LLM},
  year    = {2026},
  url     = {https://huggingface.co/datasets/IKUN-LLM/CXK_IKUN_Dataset},
  license = {Apache-2.0}
}
```
