# 几种语言模型对理解中文语义的分析比较

### ⼀、项目介绍：

针对3个不同的模型进行一些应用场景的测试，并开展不同模型之间的**横向对比**。

1. 本项目中横向对比的几个模型分别是：
- `chatglm3-6b`

- `Qwen-7B-Chat`

- `Baichuan2-7B-Base`
2. 分别询问的三个问题是：
- 请说出以下两句话区别在哪里？ 1、冬天：能穿多少穿多少 2、夏天：能穿多少穿多少

- 请说出以下两句话区别在哪里？单身狗产生的原因有两个，一是谁都看不上，二是谁都看不上

- 他知道我知道你知道他不知道吗？ 这句话里，到底谁不知道 

### 二、环境搭建：

1. 下载`conda`：
- 在终端命令行环境中输入以下列命令用于从`Anaconda`的仓库下载`Miniconda`的`Linux 64`位安装脚本：

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

- 运行下载的`Miniconda`安装脚本：

```bash
bash Miniconda3-latest-Linux-x86_64.sh -b -p /opt/conda
```

- 将`Miniconda`的`bin`目录添加到环境变量`PATH`中，并将配置追加到用户的`.bashrc`文件，以便在新的终端会话中也能使用`Miniconda`的命令：

```bash
echo 'export PATH="/opt/conda/bin:$PATH"' >> ~/.bashrc
```

- 重新加载`.bashrc`文件，使刚刚添加的环境变量配置立即生效：

```bash
source ~/.bashrc
```

2. 激活虚拟环境：

```bash
conda create-n models_env python=3.10-y
source /opt/conda/etc/profile.d/conda.sh
conda activate models_env
```

3.根据需要安装基础环境和基础依赖：（以`Qwen-7B-Chat`为例）

```bash
//基础环境安装
pip install \
 torch==2.3.0+cpu \
 torchvision==0.18.0+cpu \--index-url https://download.pytorch.org/whl/cpu

//基础依赖安装
pip install \
 "intel-extension-for-transformers==1.4.2" \
 "neural-compressor==2.5" \
 "transformers==4.33.3" \
 "modelscope==1.9.5" \
 "pydantic==1.10.13"\
 "sentencepiece" \
 "tiktoken" \
 "einops" \
 "transformers_stream_generator" \
 "uvicorn" \
 "fastapi" \
 "yacs" \
 "setuptools_scm"" \
```

### 三、模型实践：

1.模型的本地配置：

- 切换到数据目录并`git clone` 所需模型：

```bash
cd /mnt/data
git clone https://www.modelscope.cn/ZhipuAI/chatglm3-6b.git
git clone https://www.modelscope.cn/qwen/Qwen-7B-Chat.git
git clone https://www.modelscope.cn/baichuan-inc/Baichuan2-7B-Base.git
```

- 运行实例：
  
  - 切换工作目录：
  
  - 编写推理脚本`run_chatglm_cpu.py`，`run_qwen_cpu.py`，`run_baichuan_cpu.py`
    
    - 使用 `vim` 创建 `Python `脚本
    
    - 在 `vim` 中，先按 `i` 键进入插入模式，然后输入脚本代码
    
    - 输入完毕后，按 `Esc` 键退出插入模式，然后输入 `:wq` 保存并退出编辑器。

```bash
//切换目录
cd /mnt/workspace

//创建脚本文件
vim run_chatglm_cpu.py
vim run_qwen_cpu.py
vim run_baichuan_cpu.py 

//运行脚本 
python run_chatglm_cpu.py
python run_qwen_cpu.py
python run_baichuan_cpu.py      
```
