### 包/命令

torchrun: 使用torch.distributed.launch进行分布式训练(弹性启动)

fire: Python命令行解析库

PYTHONPATH: Python环境变量，指定Python模块搜索路径

accelerate: huggingface的分布式pytorch训练库

fassi: facebook 开源的向量相似度搜索库

typer: python命令行解析库

geardrails：用于LLM保护的库

[ScienceWorld](https://github.com/allenai/ScienceWorld?tab=readme-ov-file): 一个文本驱动的游戏测试环境

### 其它

operator @: Python3.5新增的矩阵乘法运算符, torch.tensive @ torch.tensive 等价于torch.matmul(torch.tensive, torch.tensive)

nn.parameter: 用于定义模型参数, 是放在Module中可训练的参数

Llama3运行脚本:

```shell
#!/bin/bash

# 模型路径
CHECKPOINT_DIR=~/.llama/checkpoints/Meta-Llama3.1-8B 

# 分布式训练，PYTHONPATH指定环境变量，torchrun指定分布式训练 
PYTHONPATH=$(git rev-parse --show-toplevel) torchrun models/scripts/example_chat_completion.py $CHECKPOINT_DIR #
```

灵感:

1. 使用LLMs作为调参工具，通过LLMs的生成能力，可以生成大量的文本数据，用于训练其他模型
2. 使用LLMs调参小模型，通过用LLMs调整超参数，可以快速调整小模型的参数，提高小模型的性能
