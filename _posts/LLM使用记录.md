
torchrun: 使用torch.distributed.launch进行分布式训练(弹性启动)

fire: Python命令行解析库

PYTHONPATH: Python环境变量，指定Python模块搜索路径

Llama3运行脚本:

```shell
#!/bin/bash

# 模型路径
CHECKPOINT_DIR=~/.llama/checkpoints/Meta-Llama3.1-8B 

# 分布式训练，PYTHONPATH指定环境变量，torchrun指定分布式训练 
PYTHONPATH=$(git rev-parse --show-toplevel) torchrun models/scripts/example_chat_completion.py $CHECKPOINT_DIR #
```
