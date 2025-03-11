---
layout: post #默认post布局

title: Markdown Template
description: 这是用于测试Jekyll主题下的Markdown模板。会被其它文章继承。
author: [diexie, ] # 此处可以简写，详细添加在 _data/authors.yml 中
date: 2024-09-08 11:33:00 +0800

pin: false # 置顶
categories: [杂项, 模板] # 分类,第一个为主分类
tags: [模板] # 标签

math: true # 支持数学公式
toc: true # 支持侧边目录
comments: true # 支持评论
mermaid: true # 支持mermaid图表

# cdn: https://xxxx.com/ # CDN加速，可以与media_subpath配合使用：[site.cdn/][page.media_subpath/]file.ext
# media_subpath: /assets/img/ # 媒体文件路径，用于简写本地图片等媒体文件路径，注意：封面图路径**会受影响**

image:
  path: https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post # 封面图
  lqip: data:image/webp # lqip占位符，用于图片懒加载
  alt: 『这是头图的描述』 # 头图描述
---

> 该文档参考至 [模板说明](https://chirpy.cotes.page/posts/write-a-new-post/)
{: .prompt-tip }

> 由于该网页基于Jekyll主题(由Liquid编写),因此支持在Markdown中使用[Liquid标签](https://jekyllrb.com/docs/liquid/tags/)和 [Liquid相关语法](https://shopify.github.io/liquid/tags/control-flow/)
{: .prompt-tip } 

> 更多源生Markdown语法请参考：[Markdown Guide](https://www.markdownguide.org/) 和 [菜鸟教程](https://www.runoob.com/markdown/md-tutorial.html)
{: .prompt-tip }

> 本地测试使用command: `bundle exec jekyll s`
{: .prompt-tip }

## 原生Markdown

----------

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题

---------

### 图片插入

本地图片(建议还是写全路径)：

![img](/assets/img/default.png) 

-------

网络图片：

![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post)

### 表格

长表格：

| 表头1 | 表头2 | 表头3 | 表头4 | 表头5 | 表头6 | 表头7 | 表头1 | 表头2 | 表头3 | 表头4 | 表头5 | 表头6 | 表头7 |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| 内容1 | 内容2 | 内容3 | 内容4 | 内容5 | 内容6 | 内容7 | 内容1 | 内容2 | 内容3 | 内容4 | 内容5 | 内容6 | 内容7 |

简单表格：

| 表头1 | 表头2 | 表头3 |
| ----- | ----- | ----- |
| 内容1 | 内容2 | 内容3 |

### 列表

#### 无序列表

- 无序列表1
- 无序列表2
- 无序列表3
  
#### 有序列表

1. 有序列表1
2. 有序列表2
3. 有序列表3

#### 混合/嵌套列表

1. 有序列表1
   - 无序列表1
   - 无序列表2
      1. 有序列表1
      2. 有序列表2

2. 有序列表2
   1. 有序列表3
      * 无序列表4
        * 无序列表5
          * 无序列表6

#### TODO列表

- [x] 已完成任务
- [ ] 未完成任务
  - [ ] 未完成子任务

### 引用/链接

[这是一个链接](https://www.google.com)

[这是一个引用][1]

[1]: https://www.google.com

### LaTeX公式

这是一个行内公式：$E=mc^2$

这是一个块级公式：

$$
E=mc^2
$$

### 代码块

```python
def hello():
    print("Hello, World!")
```

```cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

```hlsl
#include "UnityCG.cginc"
#include "Lighting.cginc"

#pragma vertex vert
#pragma fragment frag

CBUFFER_START(UnityPerMaterial)
    float4x4 unity_ObjectToWorld;
CBUFFER_END

struct appdata {
    float4 vertex : POSITION;
};

struct v2f {
    float4 vertex : SV_POSITION;
};

appdata vertex vert(appdata v) {
    v2f o;
    o.vertex = UnityObjectToClipPos(v.vertex);
    return o;
}

half4 fragment frag(v2f i) : SV_Target {
    return float4(1, 1, 1, 1);
}
```

这是一段行内代码：`print("Hello, World!")`

这是一段支持高亮的文件路径：`/path/to/file`{: .filepath}

## Jekyll扩展特性

### 图片相关

#### 图片宽高设置

{:width="100px" height="100px"}:

![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){:width="100px" height="100px"}

{:width="50%" height="50%"}:

![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){:width="50%" height="50%"}

#### 图片位置

1测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字

![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){: .normal width="50%" height="50%" }
_{: .normal}:(左对齐，文字上下排列)_

3测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字
4测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字
5测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字
![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){: .left w="50%" h="50%"}
_{: .left}: (左对齐，文字环绕)_
5测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字
6测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字 
7测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字 
![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){: .right width="50%" height="50%"}
_{: .right} (右对齐，文字环绕)_
8测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字
9测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字
1测试用文字测试用文字测试用文字测试用文字测试用文字测试用文字

#### 图片描述

![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){:width="100px" height="100px"}
_这是图片的描述_

#### 黑暗/明亮模式图片

仅黑暗模式显示：

![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){:width="100px" height="100px" .dark}

仅明亮模式显示：

![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){:width="100px" height="100px" .light}

#### 图片阴影

![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){:width="100px" height="100px" .shadow}

#### 图片占位符LQIP

Lqip用于图片懒加载，用于在图像完全加载之前显示在页面上。它通常是图像的模糊版本，或者是一个简单的占位符形状（如矩形或圆形），其主要目的是在图像加载过程中提供视觉反馈，防止页面出现空白。[^1]

十分推荐使用，可以有效提升用户体验。[^2]

![img](https://picx.zhimg.com/70/v2-eaec95835ad51dbdb0ed240cae7dc4f1_1440w.avis?source=172ae18b&biz_tag=Post){: lqip=data:image/webp}

### 提示框

> An example showing the `tip` type prompt.
{: .prompt-tip }

> An example showing the `info` type prompt.
{: .prompt-info }

> An example showing the `warning` type prompt.
{: .prompt-warning }

> An example showing the `danger` type prompt.
{: .prompt-danger }

### 视频内嵌入

语法:

```liquid
{ % include embed/{Platform}.html id='{ID}' %}
```

URL示例:

| Video URL                                                       | Platform | ID                              |
| --------------------------------------------------------------- | -------- | ------------------------------- |
| https://www.youtube.com/watch?v=Ap0huJwyT7g?si=4BN5GglyU76yf-OL | YouTube  | Ap0huJwyT7g?si=4BN5GglyU76yf-OL |
| https://www.bilibili.com/video/BV1Zj411D7so                     | Bilibili | BV1Zj411D7so                    |
| https://www.twitch.tv/videos/1634779211                         | Twitch   | 1634779211                      |

YouTube视频：

其中id为视频的id，可以在视频链接中找到，如：`https://www.youtube.com/watch?v=Ap0huJwyT7g?si=4BN5GglyU76yf-OL`中的`Ap0huJwyT7g?si=4BN5GglyU76yf-OL`

{% include embed/youtube.html id='Ap0huJwyT7g?si=4BN5GglyU76yf-OL' %}

Bilibili视频：

{% include embed/bilibili.html id='BV1Zj411D7so' %}

twitch视频：

{% include embed/twitch.html id='1634779211' %}

如果要自定义/本地插入视频：

遵循以下语法：

```liquid
{ % include embed/video.html src='{URL}' %}
```

插入视频所支持的属性：

* poster='/path/to/poster.png' — 这是在视频下载时显示的视频封面图像的路径
* title='Text' — 这是显示在视频下方的视频标题
* autoplay=true — 视频会在加载完成后立即自动播放
* loop=true — 是否循环播放
* muted=true — 是否初始为静音
* types — 指定由 | 分隔的额外视频格式的扩展名。确保这些文件存在于主视频文件的同一目录中。

完整格式如下：

```liquid
{ %
  include embed/video.html
  src='/path/to/video.mp4'
  types='ogg|mov'
  poster='poster.png'
  title='Demo video'
  autoplay=true
  loop=true
  muted=true
%}
```

### 音频内嵌入

{% include embed/audio.html url='https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3' %}

音频内嵌入语法：

```liquid
{ % include embed/audio.html url='{URL}' %}
```

完整格式如下：

```liquid
{ %
  include embed/audio.html
  src='/path/to/audio.mp3'
  types='ogg|wav|aac'
  title='Demo audio'
%}
```

### 脚注引用

始终会显示在文章末尾:

[^1]: 这是一个文内链接

[^2]: 这是另一个文内链接
