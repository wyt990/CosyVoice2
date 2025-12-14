# CosyVoice API 调用指南

## 概述

CosyVoice 提供了 FastAPI 服务器用于 API 调用。本文档详细说明如何启动 API 服务器以及如何调用各个 API 端点。

## 启动 API 服务器

### 基本启动命令

```bash
python3 runtime/python/fastapi/server.py --port 50000 --model_dir pretrained_models/CosyVoice-300M-Instruct --gpu 0
```

### 参数说明

- `--port`: 服务器端口号（默认：50000）
- `--model_dir`: 模型目录路径或 ModelScope 仓库ID（默认：iic/CosyVoice-300M）
- `--gpu`: GPU 设备ID（可选，例如：0 或 1。如果不指定，使用默认 GPU）

### 示例

```bash
# 使用本地模型路径，指定GPU 0
python3 runtime/python/fastapi/server.py --port 50000 --model_dir pretrained_models/CosyVoice-300M-Instruct --gpu 0

# 使用 ModelScope 仓库ID
python3 runtime/python/fastapi/server.py --port 50000 --model_dir iic/CosyVoice-300M --gpu 0

# 不指定GPU，使用默认GPU
python3 runtime/python/fastapi/server.py --port 50000 --model_dir pretrained_models/CosyVoice-300M-Instruct
```

## API 端点说明

FastAPI 服务器提供以下 API 端点，所有端点都支持 GET 和 POST 请求：

### 1. 预训练音色模式 (`/inference_sft`)

使用预训练的语音风格进行文本转语音合成。

#### 请求参数

- `tts_text` (str, required): 要合成的文本
- `spk_id` (str, required): 预训练音色ID（例如："中文女"、"中文男"等）

#### cURL 示例

```bash
curl -X POST "http://localhost:50000/inference_sft" \
  -F "tts_text=你好，我是通义千问语音合成大模型，请问有什么可以帮您的吗？" \
  -F "spk_id=中文女" \
  --output output.wav
```

#### Python requests 示例

```python
import requests

url = "http://localhost:50000/inference_sft"
payload = {
    'tts_text': '你好，我是通义千问语音合成大模型',
    'spk_id': '中文女'
}

response = requests.post(url, data=payload, stream=True)

# 保存音频文件
with open('output.wav', 'wb') as f:
    for chunk in response.iter_content(chunk_size=8192):
        if chunk:
            f.write(chunk)
```

---

### 2. 3s极速复刻模式 (`/inference_zero_shot`)

使用 prompt 音频和 prompt 文本进行零样本语音复刻。

#### 请求参数

- `tts_text` (str, required): 要合成的文本
- `prompt_text` (str, required): prompt文本，需与prompt音频内容一致
- `prompt_wav` (file, required): prompt音频文件（WAV格式，采样率不低于16kHz，建议不超过30秒）

#### cURL 示例

```bash
curl -X POST "http://localhost:50000/inference_zero_shot" \
  -F "tts_text=希望你以后能够做的比我还好呦" \
  -F "prompt_text=希望你以后能够做的比我还好呦" \
  -F "prompt_wav=@prompt_audio.wav" \
  --output output.wav
```

#### Python requests 示例

```python
import requests

url = "http://localhost:50000/inference_zero_shot"
payload = {
    'tts_text': '希望你以后能够做的比我还好呦',
    'prompt_text': '希望你以后能够做的比我还好呦'
}
files = {
    'prompt_wav': ('prompt_audio.wav', open('prompt_audio.wav', 'rb'), 'audio/wav')
}

response = requests.post(url, data=payload, files=files, stream=True)

# 保存音频文件
with open('output.wav', 'wb') as f:
    for chunk in response.iter_content(chunk_size=8192):
        if chunk:
            f.write(chunk)
```

---

### 3. 跨语种复刻模式 (`/inference_cross_lingual`)

使用 prompt 音频进行跨语种语音复刻（合成文本和 prompt 音频应为不同语言）。

#### 请求参数

- `tts_text` (str, required): 要合成的文本（不同语言）
- `prompt_wav` (file, required): prompt音频文件（WAV格式，采样率不低于16kHz）

#### cURL 示例

```bash
curl -X POST "http://localhost:50000/inference_cross_lingual" \
  -F "tts_text=Hello, this is a cross-lingual text-to-speech test" \
  -F "prompt_wav=@prompt_audio_chinese.wav" \
  --output output.wav
```

#### Python requests 示例

```python
import requests

url = "http://localhost:50000/inference_cross_lingual"
payload = {
    'tts_text': 'Hello, this is a cross-lingual test'
}
files = {
    'prompt_wav': ('prompt_audio.wav', open('prompt_audio.wav', 'rb'), 'audio/wav')
}

response = requests.post(url, data=payload, files=files, stream=True)

# 保存音频文件
with open('output.wav', 'wb') as f:
    for chunk in response.iter_content(chunk_size=8192):
        if chunk:
            f.write(chunk)
```

---

### 4. 自然语言控制模式 (`/inference_instruct`)

使用自然语言指令控制语音生成，需要 CosyVoice-300M-Instruct 模型。

#### 请求参数

- `tts_text` (str, required): 要合成的文本
- `spk_id` (str, required): 预训练音色ID
- `instruct_text` (str, required): 自然语言指令文本（描述希望的声音风格、情感等）

#### cURL 示例

```bash
curl -X POST "http://localhost:50000/inference_instruct" \
  -F "tts_text=Hello, I am a test" \
  -F "spk_id=中文女" \
  -F "instruct_text=Speak with a cheerful and energetic tone" \
  --output output.wav
```

#### Python requests 示例

```python
import requests

url = "http://localhost:50000/inference_instruct"
payload = {
    'tts_text': 'Hello, I am a test',
    'spk_id': '中文女',
    'instruct_text': 'Speak with a cheerful and energetic tone'
}

response = requests.post(url, data=payload, stream=True)

# 保存音频文件
with open('output.wav', 'wb') as f:
    for chunk in response.iter_content(chunk_size=8192):
        if chunk:
            f.write(chunk)
```

---

### 5. Instruct2模式 (`/inference_instruct2`)

使用自然语言指令和 prompt 音频进行语音生成。

#### 请求参数

- `tts_text` (str, required): 要合成的文本
- `instruct_text` (str, required): 自然语言指令文本
- `prompt_wav` (file, required): prompt音频文件（WAV格式，采样率不低于16kHz）

#### cURL 示例

```bash
curl -X POST "http://localhost:50000/inference_instruct2" \
  -F "tts_text=Hello, I am a test" \
  -F "instruct_text=Speak with a cheerful and energetic tone" \
  -F "prompt_wav=@prompt_audio.wav" \
  --output output.wav
```

#### Python requests 示例

```python
import requests

url = "http://localhost:50000/inference_instruct2"
payload = {
    'tts_text': 'Hello, I am a test',
    'instruct_text': 'Speak with a cheerful and energetic tone'
}
files = {
    'prompt_wav': ('prompt_audio.wav', open('prompt_audio.wav', 'rb'), 'audio/wav')
}

response = requests.post(url, data=payload, files=files, stream=True)

# 保存音频文件
with open('output.wav', 'wb') as f:
    for chunk in response.iter_content(chunk_size=8192):
        if chunk:
            f.write(chunk)
```

---

## 使用官方客户端

项目提供了一个命令行客户端工具，可以直接调用 API：

```bash
python3 runtime/python/fastapi/client.py \
  --host localhost \
  --port 50000 \
  --mode sft \
  --tts_text "你好，我是通义千问语音合成大模型" \
  --spk_id "中文女" \
  --tts_wav output.wav
```

### 客户端参数说明

- `--host`: 服务器地址（默认：0.0.0.0）
- `--port`: 服务器端口（默认：50000）
- `--mode`: 请求模式，可选值：`sft`, `zero_shot`, `cross_lingual`, `instruct`
- `--tts_text`: 要合成的文本
- `--spk_id`: 预训练音色ID（sft 和 instruct 模式需要）
- `--prompt_text`: prompt文本（zero_shot 模式需要）
- `--prompt_wav`: prompt音频文件路径（zero_shot、cross_lingual 模式需要）
- `--instruct_text`: 自然语言指令文本（instruct 模式需要）
- `--tts_wav`: 输出音频文件路径

### 客户端使用示例

```bash
# 预训练音色模式
python3 runtime/python/fastapi/client.py \
  --host localhost \
  --port 50000 \
  --mode sft \
  --tts_text "你好，我是通义千问语音合成大模型" \
  --spk_id "中文女" \
  --tts_wav output_sft.wav

# 3s极速复刻模式
python3 runtime/python/fastapi/client.py \
  --host localhost \
  --port 50000 \
  --mode zero_shot \
  --tts_text "希望你以后能够做的比我还好呦" \
  --prompt_text "希望你以后能够做的比我还好呦" \
  --prompt_wav prompt_audio.wav \
  --tts_wav output_zero_shot.wav

# 跨语种复刻模式
python3 runtime/python/fastapi/client.py \
  --host localhost \
  --port 50000 \
  --mode cross_lingual \
  --tts_text "Hello, this is a cross-lingual test" \
  --prompt_wav prompt_audio.wav \
  --tts_wav output_cross_lingual.wav

# 自然语言控制模式
python3 runtime/python/fastapi/client.py \
  --host localhost \
  --port 50000 \
  --mode instruct \
  --tts_text "Hello, I am a test" \
  --spk_id "中文女" \
  --instruct_text "Speak with a cheerful and energetic tone" \
  --tts_wav output_instruct.wav
```

---

## 响应格式

所有 API 端点返回流式音频数据：
- 格式：WAV格式，16位PCM编码
- 采样率：通常为 22050 Hz（具体取决于模型配置）
- 传输方式：流式传输（Streaming Response）
- Content-Type: `application/octet-stream` 或 `audio/wav`

响应数据可以直接保存为 `.wav` 文件进行播放。

---

## 注意事项

1. **模型选择**：
   - 使用 `instruct` 或 `inference_instruct2` 模式时，需要 CosyVoice-300M-Instruct 模型
   - 使用 `cross_lingual` 模式时，需要 CosyVoice-300M 模型（非 Instruct 版本）

2. **音频文件要求**：
   - prompt 音频文件应为 WAV 格式
   - 采样率不低于 16kHz
   - 建议音频时长不超过 30 秒

3. **CORS 支持**：
   - FastAPI 服务器已配置 CORS 中间件，允许跨域请求
   - 允许所有来源（`allow_origins=["*"]`）

4. **并发限制**：
   - 默认情况下，服务器可以处理多个并发请求
   - 如果遇到性能问题，可以考虑使用负载均衡或限制并发数

5. **GPU 使用**：
   - 确保指定的 GPU 设备可用
   - 如果 CUDA 不可用，服务器会自动回退到 CPU（性能会显著降低）

---

## 故障排查

### 常见问题

1. **连接被拒绝**：
   - 检查服务器是否已启动
   - 确认端口号是否正确
   - 检查防火墙设置

2. **GPU 相关错误**：
   - 确认 GPU 设备ID是否有效
   - 检查 CUDA 是否正确安装
   - 验证 GPU 是否被其他进程占用

3. **模型加载失败**：
   - 确认模型路径是否正确
   - 检查模型文件是否完整
   - 如果是 ModelScope 仓库ID，确保网络连接正常

4. **音频生成失败**：
   - 检查输入参数是否正确
   - 确认 prompt 音频格式是否符合要求
   - 查看服务器日志获取详细错误信息

---

## 相关文档

- [README.md](../README.md) - 项目总体说明
- [conda使用方法.md](./conda使用方法.md) - 环境配置说明
