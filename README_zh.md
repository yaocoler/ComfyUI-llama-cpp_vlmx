# ComfyUI-llama-cpp
在 ComfyUI 中基于 llama.cpp 框架原生运行 LLM & VLM 模型。  
**[[📃English](./README.md)]**   

## 预览
![](./img/preview.jpg) 

## Text to Image Prompt 节点

该节点默认只执行透明的 LLM 调用：

```text
System Prompt → User Prompt → llama.cpp → Prompt
```

默认不会加入隐藏的分析、推理、规划、自检、思维链、翻译或格式化 Prompt。

- `Internal Prompt Engineering`：默认 `Disabled`，仅在主动开启后使用节点
  自带的简短图像 Prompt 优化指令。
- `Raw Mode`：开启后强制关闭内部增强，输入原样发送，响应原样返回。
- `Output Mode`：默认 `Raw`；`Text` 只清理首尾空白，`JSON` 只验证格式。
- `Language`：默认 `Auto`，仅在内部增强开启时作为语言建议。

旧版 `Subject`、`Setting Words` 输入已改为 `System Prompt`、`User Prompt`。
旧工作流首次打开时需要重新填写这些字段和新增选项。

## 安装步骤

#### 安装节点:
```bash
cd ComfyUI/custom_nodes
git clone https://github.com/lihaoyun6/ComfyUI-llama-cpp.git
python -m pip install -r ComfyUI-llama-cpp/requirements.txt
```

### 模型路径:
- 请将下载的 `.gguf` 模型放置在 `ComfyUI/models/LLM` 目录中.  

	> 在使用VLM模型进行图像推理之前, 请确保已经下载并选择了主模型对应的`mmproj`权重文件.

## 致谢
- [llama-cpp-python](https://github.com/JamePeng/llama-cpp-python) @JamePeng  
- [ComfyUI-llama-cpp](https://github.com/kijai/ComfyUI-llama-cpp) @kijai
- [ComfyUI](https://github.com/comfyanonymous/ComfyUI) @comfyanonymous
