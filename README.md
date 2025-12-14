[![SVG Banners](https://svg-banners.vercel.app/api?type=origin&text1=CosyVoice🤠&text2=Text-to-Speech%20💖%20Large%20Language%20Model&width=800&height=210)](https://github.com/Akshay090/svg-banners)

## 👉🏻 CosyVoice 👈🏻

**CosyVoice 3.0**: [演示](https://funaudiollm.github.io/cosyvoice3/); [论文](https://arxiv.org/abs/2505.17589); [CV3-Eval](https://github.com/FunAudioLLM/CV3-Eval)

**CosyVoice 2.0**: [演示](https://funaudiollm.github.io/cosyvoice2/); [论文](https://arxiv.org/abs/2412.10117); [ModelScope](https://www.modelscope.cn/studios/iic/CosyVoice2-0.5B); [HuggingFace](https://huggingface.co/spaces/FunAudioLLM/CosyVoice2-0.5B)

**CosyVoice 1.0**: [演示](https://fun-audio-llm.github.io); [论文](https://funaudiollm.github.io/pdf/CosyVoice_v1.pdf); [ModelScope](https://www.modelscope.cn/studios/iic/CosyVoice-300M)

## 亮点🔥

**CosyVoice 2.0** 已发布！相比 1.0 版本，新版本提供了更准确、更稳定、更快、更好的语音生成能力。

### 多语言支持
- **支持语言**: 中文、英文、日文、韩文、中文方言（粤语、四川话、上海话、天津话、武汉话等）
- **跨语言和混合语言**: 支持跨语言和代码切换场景的零样本语音克隆。

### 超低延迟
- **双向流式支持**: CosyVoice 2.0 集成了离线和流式建模技术。
- **快速首包合成**: 在保持高质量音频输出的同时，延迟低至 150ms。

### 高准确率
- **改进的发音**: 相比 CosyVoice 1.0，发音错误率降低 30% 至 50%。
- **基准测试成就**: 在 Seed-TTS 评估集的困难测试集上达到最低字符错误率。

### 强稳定性
- **音色一致性**: 确保零样本和跨语言语音合成的可靠音色一致性。
- **跨语言合成**: 相比 1.0 版本有显著改进。

### 自然体验
- **增强的韵律和音质**: 改进了合成音频的对齐，MOS 评估分数从 5.4 提升到 5.53。
- **情感和方言灵活性**: 现在支持更细粒度的情感控制和口音调整。

## 路线图

- [x] 2025/08
    - [x] 感谢 NVIDIA Yuekai Zhang 的贡献，添加了 triton trtllm 运行时支持和 cosyvoice2 grpo 训练支持

- [x] 2025/07
    - [x] 发布 cosyvoice 3.0 评估集

- [x] 2025/05
    - [x] 添加 cosyvoice 2.0 vllm 支持

- [x] 2024/12
    - [x] 25hz cosyvoice 2.0 发布

- [x] 2024/09
    - [x] 25hz cosyvoice 基础模型
    - [x] 25hz cosyvoice 语音转换模型

- [x] 2024/08
    - [x] 用于 LLM 稳定性的重复感知采样(RAS)推理
    - [x] 流式推理模式支持，包括用于 RTF 优化的 kv cache 和 sdpa

- [x] 2024/07
    - [x] Flow matching 训练支持
    - [x] 当 ttsfrd 不可用时支持 WeTextProcessing
    - [x] Fastapi 服务器和客户端

## 模型对比分析

### 可用模型概览

CosyVoice 项目提供了多个预训练模型，每个模型针对不同的使用场景进行了优化。以下是详细的模型对比分析：

| 模型 | 参数量 | 推荐度 | 主要用途 | 显存需求 | 版本 |
|------|--------|--------|----------|----------|------|
| **CosyVoice2-0.5B** | 0.5B | ⭐⭐⭐⭐⭐ | 通用（最佳性能） | 高 | 2.0 |
| **CosyVoice-300M** | 300M | ⭐⭐⭐⭐ | 零样本、跨语种、VC | 中 | 1.0 |
| **CosyVoice-300M-SFT** | 300M | ⭐⭐⭐ | 固定音色场景 | 中 | 1.0 |
| **CosyVoice-300M-Instruct** | 300M | ⭐⭐⭐⭐ | 情感/风格控制 | 中 | 1.0 |
| **CosyVoice-300M-25Hz** | 300M | ⭐⭐⭐ | 实时/快速推理 | 低 | 1.0 |

### 功能支持矩阵

| 功能 | CosyVoice2-0.5B | CosyVoice-300M | 300M-SFT | 300M-Instruct |
|------|------------------|----------------|----------|---------------|
| Zero-shot 语音克隆 | ✅ | ✅ | ❌ | ❌ |
| 跨语种合成 | ✅ | ✅ | ❌ | ❌ |
| SFT（预训练音色） | ❌ | ❌ | ✅ | ✅ |
| Instruct 自然语言控制 | ✅ (instruct2) | ❌ | ❌ | ✅ |
| 语音转换（VC） | ❌ | ✅ | ❌ | ❌ |
| 流式推理 | ✅ | ✅ | ✅ | ✅ |

### 详细模型分析

#### 1. CosyVoice2-0.5B ⭐⭐⭐⭐⭐（推荐）

**版本**: CosyVoice 2.0  
**参数量**: 0.5B  
**架构**: 基于 Qwen2 的大语言模型

**特点**:
- ✅ **最佳性能**: 官方强烈推荐，性能最优
- ✅ **超低延迟**: 首包延迟低至 150ms
- ✅ **高准确率**: 发音错误率比 1.0 版本降低 30-50%
- ✅ **强稳定性**: 零样本和跨语言合成稳定性显著提升
- ✅ **流式推理**: 支持双向流式推理
- ✅ **多语言支持**: 中文、英文、日文、韩文、中文方言等
- ✅ **高质量**: MOS 评分 5.53（1.0 版本为 5.4）

**支持的功能**:
- Zero-shot 语音克隆（3s 极速复刻）
- 跨语种合成
- 细粒度控制（如 `[laughter]` 标记）
- Instruct 模式（自然语言控制，使用 `inference_instruct2`）
- 双向流式推理

**优点**:
- ✅ 性能最佳，准确率最高
- ✅ 延迟最低，适合实时场景
- ✅ 稳定性强，音色一致性好
- ✅ 支持 vLLM 加速推理
- ✅ 支持 TensorRT-LLM 加速（4倍加速）

**缺点**:
- ❌ 模型较大（0.5B vs 300M），显存占用更高
- ❌ 不支持 `inference_instruct`（仅支持 `inference_instruct2`）
- ❌ 不支持语音转换（VC）功能

**适用场景**: 追求最佳性能的通用场景，实时语音合成，高质量零样本克隆

---

#### 2. CosyVoice-300M（基础版）

**版本**: CosyVoice 1.0  
**参数量**: 300M  
**架构**: 基于 Transformer

**特点**:
- 基础模型，功能完整
- 支持多种推理模式

**支持的功能**:
- Zero-shot 语音克隆
- 跨语种合成（需要使用语言标签如 `<|zh|>`, `<|en|>`）
- 语音转换（VC）
- ❌ 不支持 SFT 和 Instruct（需要使用对应的变体模型）

**优点**:
- ✅ 模型较小，显存占用低
- ✅ 功能覆盖全面
- ✅ 支持语音转换功能
- ✅ 兼容性好，稳定可靠

**缺点**:
- ❌ 性能不如 2.0 版本
- ❌ 准确率相对较低
- ❌ 不支持流式推理优化
- ❌ 不支持 Instruct 模式

**适用场景**: 需要语音转换的场景，资源受限的环境，基础语音合成需求

---

#### 3. CosyVoice-300M-SFT

**版本**: CosyVoice 1.0  
**参数量**: 300M  
**架构**: 基于 Transformer（SFT 微调版本）

**特点**:
- 基于 CosyVoice-300M 的 SFT（Supervised Fine-Tuning）微调版本
- 内置预训练音色库

**支持的功能**:
- SFT 模式（使用预训练音色）
- 支持 `list_available_spks()` 查看可用音色列表
- ❌ 不支持 Zero-shot、跨语种、VC、Instruct

**优点**:
- ✅ 预训练音色质量稳定可靠
- ✅ 无需提供 prompt 音频，使用方便
- ✅ 适合固定音色场景

**缺点**:
- ❌ 音色选择有限，只能使用预训练音色
- ❌ 不支持自定义音色克隆
- ❌ 不支持跨语种合成

**适用场景**: 固定音色场景，客服系统，标准化语音输出

---

#### 4. CosyVoice-300M-Instruct

**版本**: CosyVoice 1.0  
**参数量**: 300M  
**架构**: 基于 Transformer（指令微调版本）

**特点**:
- 基于 CosyVoice-300M 的指令微调版本
- 支持自然语言控制

**支持的功能**:
- Instruct 模式（自然语言控制）
- 支持情感、角色等细粒度控制
- 支持特殊标记：`<laughter>`, `<strong>`, `[breath]` 等
- 支持 SFT 模式（使用预训练音色）
- ❌ 不支持跨语种、VC

**优点**:
- ✅ 支持细粒度情感和风格控制
- ✅ 可以通过描述角色特征进行控制
- ✅ 适合需要情感表达的场景

**缺点**:
- ❌ 不支持跨语种合成
- ❌ 不支持语音转换
- ❌ 需要提供角色描述文本

**适用场景**: 需要情感控制的场景，角色扮演，有声书制作

---

#### 5. CosyVoice-300M-25Hz

**版本**: CosyVoice 1.0（25Hz 变体）  
**参数量**: 300M  
**架构**: 基于 Transformer（25Hz 帧率版本）

**特点**:
- 25Hz 帧率版本（标准版本为 50Hz）
- 推理速度更快，质量略有下降

**优点**:
- ✅ 推理速度更快
- ✅ 显存占用更低
- ✅ 适合实时场景

**缺点**:
- ❌ 音质可能略低于 50Hz 版本
- ❌ 文档中信息较少

**适用场景**: 实时语音合成，资源受限环境，快速推理需求

---

#### 6. CosyVoice-ttsfrd（资源文件）

**类型**: 文本处理资源  
**用途**: 文本规范化

**特点**:
- 非模型文件，是文本处理资源
- 用于提升文本规范化性能
- 可选安装（不安装则使用 wetext 作为默认）

---

### 模型选择建议

1. **追求最佳性能**: 选择 **CosyVoice2-0.5B**
2. **需要语音转换**: 选择 **CosyVoice-300M**
3. **固定音色场景**: 选择 **CosyVoice-300M-SFT**
4. **需要情感控制**: 选择 **CosyVoice-300M-Instruct**
5. **资源受限环境**: 选择 **CosyVoice-300M-25Hz**

## 安装

### 克隆和安装

- 克隆仓库
    ``` sh
    git clone --recursive https://github.com/FunAudioLLM/CosyVoice.git
    # 如果由于网络故障无法克隆子模块，请运行以下命令直到成功
    cd CosyVoice
    git submodule update --init --recursive
    ```

- 安装 Conda: 请参阅 https://docs.conda.io/en/latest/miniconda.html
- 创建 Conda 环境:

    ``` sh
    conda create -n cosyvoice -y python=3.10
    conda activate cosyvoice
    pip install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/ --trusted-host=mirrors.aliyun.com

    # 如果遇到 sox 兼容性问题
    # ubuntu
    sudo apt-get install sox libsox-dev
    # centos
    sudo yum install sox sox-devel
    ```

### 模型下载

我们强烈建议您下载我们的预训练模型 `CosyVoice2-0.5B` `CosyVoice-300M` `CosyVoice-300M-SFT` `CosyVoice-300M-Instruct` 以及 `CosyVoice-ttsfrd` 资源。

``` python
# SDK 模型下载
from modelscope import snapshot_download
snapshot_download('iic/CosyVoice2-0.5B', local_dir='pretrained_models/CosyVoice2-0.5B')
snapshot_download('iic/CosyVoice-300M', local_dir='pretrained_models/CosyVoice-300M')
snapshot_download('iic/CosyVoice-300M-SFT', local_dir='pretrained_models/CosyVoice-300M-SFT')
snapshot_download('iic/CosyVoice-300M-Instruct', local_dir='pretrained_models/CosyVoice-300M-Instruct')
snapshot_download('iic/CosyVoice-ttsfrd', local_dir='pretrained_models/CosyVoice-ttsfrd')
```

``` sh
# git 模型下载，请确保已安装 git lfs
mkdir -p pretrained_models
git clone https://www.modelscope.cn/iic/CosyVoice2-0.5B.git pretrained_models/CosyVoice2-0.5B
git clone https://www.modelscope.cn/iic/CosyVoice-300M.git pretrained_models/CosyVoice-300M
git clone https://www.modelscope.cn/iic/CosyVoice-300M-SFT.git pretrained_models/CosyVoice-300M-SFT
git clone https://www.modelscope.cn/iic/CosyVoice-300M-Instruct.git pretrained_models/CosyVoice-300M-Instruct
git clone https://www.modelscope.cn/iic/CosyVoice-ttsfrd.git pretrained_models/CosyVoice-ttsfrd

modelscope download --model iic/CosyVoice-300M-SFT --local_dir ./CosyVoice-300M-SFT
modelscope download --model iic/CosyVoice-300M-Instruct --local_dir ./CosyVoice-300M-Instruct
modelscope download --model iic/CosyVoice-ttsfrd --local_dir ./CosyVoice-ttsfrd

```

可选地，您可以解压 `ttsfrd` 资源并安装 `ttsfrd` 包以获得更好的文本规范化性能。

注意：此步骤不是必需的。如果您不安装 `ttsfrd` 包，我们将默认使用 wetext。

``` sh
cd pretrained_models/CosyVoice-ttsfrd/
unzip resource.zip -d .
pip install ttsfrd_dependency-0.1-py3-none-any.whl
pip install ttsfrd-0.4.2-cp310-cp310-linux_x86_64.whl
```

### 基本使用

我们强烈建议使用 `CosyVoice2-0.5B` 以获得更好的性能。
请按照以下代码了解每个模型的详细使用方法。

``` python
import sys
sys.path.append('third_party/Matcha-TTS')
from cosyvoice.cli.cosyvoice import CosyVoice, CosyVoice2
from cosyvoice.utils.file_utils import load_wav
import torchaudio
```

#### CosyVoice2 使用示例
```python
cosyvoice = CosyVoice2('pretrained_models/CosyVoice2-0.5B', load_jit=False, load_trt=False, load_vllm=False, fp16=False)

# 注意：如果您想复现 https://funaudiollm.github.io/cosyvoice2 上的结果，请在推理时添加 text_frontend=False
# zero_shot 使用
prompt_speech_16k = load_wav('./asset/zero_shot_prompt.wav', 16000)
for i, j in enumerate(cosyvoice.inference_zero_shot('收到好友从远方寄来的生日礼物，那份意外的惊喜与深深的祝福让我心中充满了甜蜜的快乐，笑容如花儿般绽放。', '希望你以后能够做的比我还好呦。', prompt_speech_16k, stream=False)):
    torchaudio.save('zero_shot_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)

# 保存 zero_shot 音色以供将来使用
assert cosyvoice.add_zero_shot_spk('希望你以后能够做的比我还好呦。', prompt_speech_16k, 'my_zero_shot_spk') is True
for i, j in enumerate(cosyvoice.inference_zero_shot('收到好友从远方寄来的生日礼物，那份意外的惊喜与深深的祝福让我心中充满了甜蜜的快乐，笑容如花儿般绽放。', '', '', zero_shot_spk_id='my_zero_shot_spk', stream=False)):
    torchaudio.save('zero_shot_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)
cosyvoice.save_spkinfo()

# 细粒度控制，支持的控件请查看 cosyvoice/tokenizer/tokenizer.py#L248
for i, j in enumerate(cosyvoice.inference_cross_lingual('在他讲述那个荒诞故事的过程中，他突然[laughter]停下来，因为他自己也被逗笑了[laughter]。', prompt_speech_16k, stream=False)):
    torchaudio.save('fine_grained_control_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)

# instruct 使用
for i, j in enumerate(cosyvoice.inference_instruct2('收到好友从远方寄来的生日礼物，那份意外的惊喜与深深的祝福让我心中充满了甜蜜的快乐，笑容如花儿般绽放。', '用四川话说这句话', prompt_speech_16k, stream=False)):
    torchaudio.save('instruct_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)

# 双向流式使用，您可以使用生成器作为输入，这在将文本 LLM 模型作为输入时很有用
# 注意：您仍然需要一些基本的句子分割逻辑，因为 LLM 无法处理任意长度的句子
def text_generator():
    yield '收到好友从远方寄来的生日礼物，'
    yield '那份意外的惊喜与深深的祝福'
    yield '让我心中充满了甜蜜的快乐，'
    yield '笑容如花儿般绽放。'
for i, j in enumerate(cosyvoice.inference_zero_shot(text_generator(), '希望你以后能够做的比我还好呦。', prompt_speech_16k, stream=False)):
    torchaudio.save('zero_shot_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)
```

#### CosyVoice2 vllm 使用

如果您想使用 vllm 进行推理，请安装 `vllm==v0.9.0`。旧版本的 vllm 不支持 CosyVoice2 推理。

注意：`vllm==v0.9.0` 有很多特定要求，例如 `torch==2.7.0`。如果您的硬件不支持 vllm 或旧环境已损坏，您可以创建一个新环境。

``` sh
conda create -n cosyvoice_vllm --clone cosyvoice
conda activate cosyvoice_vllm
pip install vllm==v0.9.0 transformers==4.51.3 -i https://mirrors.aliyun.com/pypi/simple/ --trusted-host=mirrors.aliyun.com
python vllm_example.py
```

#### CosyVoice 使用示例
```python
cosyvoice = CosyVoice('pretrained_models/CosyVoice-300M-SFT', load_jit=False, load_trt=False, fp16=False)
# sft 使用
print(cosyvoice.list_available_spks())
# 将 stream=True 用于分块流式推理
for i, j in enumerate(cosyvoice.inference_sft('你好，我是通义生成式语音大模型，请问有什么可以帮您的吗？', '中文女', stream=False)):
    torchaudio.save('sft_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)

cosyvoice = CosyVoice('pretrained_models/CosyVoice-300M')
# zero_shot 使用，<|zh|><|en|><|jp|><|yue|><|ko|> 分别表示中文/英文/日文/粤语/韩文
prompt_speech_16k = load_wav('./asset/zero_shot_prompt.wav', 16000)
for i, j in enumerate(cosyvoice.inference_zero_shot('收到好友从远方寄来的生日礼物，那份意外的惊喜与深深的祝福让我心中充满了甜蜜的快乐，笑容如花儿般绽放。', '希望你以后能够做的比我还好呦。', prompt_speech_16k, stream=False)):
    torchaudio.save('zero_shot_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)
# cross_lingual 使用
prompt_speech_16k = load_wav('./asset/cross_lingual_prompt.wav', 16000)
for i, j in enumerate(cosyvoice.inference_cross_lingual('<|en|>And then later on, fully acquiring that company. So keeping management in line, interest in line with the asset that\'s coming into the family is a reason why sometimes we don\'t buy the whole thing.', prompt_speech_16k, stream=False)):
    torchaudio.save('cross_lingual_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)
# vc 使用
prompt_speech_16k = load_wav('./asset/zero_shot_prompt.wav', 16000)
source_speech_16k = load_wav('./asset/cross_lingual_prompt.wav', 16000)
for i, j in enumerate(cosyvoice.inference_vc(source_speech_16k, prompt_speech_16k, stream=False)):
    torchaudio.save('vc_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)

cosyvoice = CosyVoice('pretrained_models/CosyVoice-300M-Instruct')
# instruct 使用，支持 <laughter></laughter><strong></strong>[laughter][breath]
for i, j in enumerate(cosyvoice.inference_instruct('在面对挑战时，他展现了非凡的<strong>勇气</strong>与<strong>智慧</strong>。', '中文男', 'Theo \'Crimson\', is a fiery, passionate rebel leader. Fights with fervor for justice, but struggles with impulsiveness.', stream=False)):
    torchaudio.save('instruct_{}.wav'.format(i), j['tts_speech'], cosyvoice.sample_rate)
```

#### 启动 Web 演示

您可以使用我们的 Web 演示页面快速熟悉 CosyVoice。

请查看演示网站了解详细信息。

``` python
# 使用 SFT 推理时改为 iic/CosyVoice-300M-SFT，或使用 Instruct 推理时改为 iic/CosyVoice-300M-Instruct
python3 webui.py --port 50000 --model_dir pretrained_models/CosyVoice-300M
```

#### GPU 选择功能

如果您的服务器有多个 GPU，可以使用 `--gpu` 参数指定使用哪个 GPU 设备。

**使用方法**:
```bash
# 使用 GPU 1（而不是默认的 GPU 0）
python3 webui.py --port 50000 --model_dir pretrained_models/CosyVoice-300M --gpu 1

# 使用 GPU 0（默认，可以不指定）
python3 webui.py --port 50000 --model_dir pretrained_models/CosyVoice-300M --gpu 0

# 不指定 --gpu 参数时，默认使用 GPU 0
python3 webui.py --port 50000 --model_dir pretrained_models/CosyVoice-300M
```

**参数说明**:
- `--gpu`: GPU 设备 ID（例如 0 或 1）。如果不指定，默认使用 GPU 0
- 系统会自动验证指定的 GPU 是否存在，如果不存在会报错

**注意事项**:
- 确保指定的 GPU 设备可用
- 如果 CUDA 不可用，系统会忽略 `--gpu` 参数并给出警告
- 所有相关组件（PyTorch、ONNX Runtime）都会使用指定的 GPU

#### 高级使用

对于高级用户，我们在 `examples/libritts/cosyvoice/run.sh` 中提供了训练和推理脚本。

#### 构建部署版本

可选地，如果您想要服务部署，可以运行以下步骤。

``` sh
cd runtime/python
docker build -t cosyvoice:v1.0 .
# 如果要使用 instruct 推理，将 iic/CosyVoice-300M 改为 iic/CosyVoice-300M-Instruct
# 用于 grpc 使用
docker run -d --runtime=nvidia -p 50000:50000 cosyvoice:v1.0 /bin/bash -c "cd /opt/CosyVoice/CosyVoice/runtime/python/grpc && python3 server.py --port 50000 --max_conc 4 --model_dir iic/CosyVoice-300M && sleep infinity"
cd grpc && python3 client.py --port 50000 --mode <sft|zero_shot|cross_lingual|instruct>
# 用于 fastapi 使用
docker run -d --runtime=nvidia -p 50000:50000 cosyvoice:v1.0 /bin/bash -c "cd /opt/CosyVoice/CosyVoice/runtime/python/fastapi && python3 server.py --port 50000 --model_dir iic/CosyVoice-300M && sleep infinity"
cd fastapi && python3 client.py --port 50000 --mode <sft|zero_shot|cross_lingual|instruct>
```

#### 使用 Nvidia TensorRT-LLM 进行部署

使用 TensorRT-LLM 加速 cosyvoice2 llm 相比 huggingface transformers 实现可以获得 4 倍加速。
快速开始:

``` sh
cd runtime/triton_trtllm
docker compose up -d
```
更多详细信息，您可以查看 [这里](https://github.com/FunAudioLLM/CosyVoice/tree/main/runtime/triton_trtllm)

## 讨论与交流

您可以直接在 [Github Issues](https://github.com/FunAudioLLM/CosyVoice/issues) 上讨论。

您也可以扫描二维码加入我们的官方钉钉聊天群。

<img src="./asset/dingding.png" width="250px">

## 致谢

1. 我们从 [FunASR](https://github.com/modelscope/FunASR) 借鉴了大量代码。
2. 我们从 [FunCodec](https://github.com/modelscope/FunCodec) 借鉴了大量代码。
3. 我们从 [Matcha-TTS](https://github.com/shivammehta25/Matcha-TTS) 借鉴了大量代码。
4. 我们从 [AcademiCodec](https://github.com/yangdongchao/AcademiCodec) 借鉴了大量代码。
5. 我们从 [WeNet](https://github.com/wenet-e2e/wenet) 借鉴了大量代码。

## 引用

``` bibtex
@article{du2024cosyvoice,
  title={Cosyvoice: A scalable multilingual zero-shot text-to-speech synthesizer based on supervised semantic tokens},
  author={Du, Zhihao and Chen, Qian and Zhang, Shiliang and Hu, Kai and Lu, Heng and Yang, Yexin and Hu, Hangrui and Zheng, Siqi and Gu, Yue and Ma, Ziyang and others},
  journal={arXiv preprint arXiv:2407.05407},
  year={2024}
}

@article{du2024cosyvoice,
  title={Cosyvoice 2: Scalable streaming speech synthesis with large language models},
  author={Du, Zhihao and Wang, Yuxuan and Chen, Qian and Shi, Xian and Lv, Xiang and Zhao, Tianyu and Gao, Zhifu and Yang, Yexin and Gao, Changfeng and Wang, Hui and others},
  journal={arXiv preprint arXiv:2412.10117},
  year={2024}
}

@article{du2025cosyvoice,
  title={CosyVoice 3: Towards In-the-wild Speech Generation via Scaling-up and Post-training},
  author={Du, Zhihao and Gao, Changfeng and Wang, Yuxuan and Yu, Fan and Zhao, Tianyu and Wang, Hao and Lv, Xiang and Wang, Hui and Shi, Xian and An, Keyu and others},
  journal={arXiv preprint arXiv:2505.17589},
  year={2025}
}

@inproceedings{lyu2025build,
  title={Build LLM-Based Zero-Shot Streaming TTS System with Cosyvoice},
  author={Lyu, Xiang and Wang, Yuxuan and Zhao, Tianyu and Wang, Hao and Liu, Huadai and Du, Zhihao},
  booktitle={ICASSP 2025-2025 IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP)},
  pages={1--2},
  year={2025},
  organization={IEEE}
}
```

## 免责声明

上述内容仅供学术目的，旨在展示技术能力。部分示例来源于互联网。如有任何内容侵犯您的权利，请联系我们请求删除。
