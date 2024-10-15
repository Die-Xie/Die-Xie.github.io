## 有用插件记录

<!-- - vscode vim 模式下的中文分词解决方案: [源码](https://github.com/stephanoskomnenos/vscode-jieba/tree/main) 注意：该方法存在问题 -->

1. [cjk-word-handler](https://github.com/SharzyL/cjk-word-handler): 实现中文分词
  ```json
  // 以下用于兼容cjk-word-handler与vscode-vim
  // issue: https://github.com/SharzyL/cjk-word-handler/issues/5
  "vim.normalModeKeyBindings": [
    {
      "before": ["w"],
      "commands": ["cjkWordHandler.cursorWordEndRight"]
    },
    {
      "before": ["b"],
      "commands": ["cjkWordHandler.cursorWordStartLeft"]
    },
    {
      "before": ["d", "w"],
      "commands": ["cjkWordHandler.deleteWordEndRight"]
    },
    {
      "before": ["d", "b"],
      "commands": ["cjkWordHandler.deleteWordStartLeft"]
    }
    ]

    "vim.visualModeKeyBindings": [
      {
        "before": ["w"],
        "commands": ["cjkWordHandler.cursorWordEndRightSelect"]
      },
      {
        "before": ["b"],
        "commands": ["cjkWordHandler.cursorWordStartLeftSelect"]
      }
    ]
  ```

## 插件开发

[开发者中文文档](https://rackar.github.io/vscode-ext-doccn/)
