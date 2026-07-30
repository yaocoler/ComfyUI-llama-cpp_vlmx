# ComfyUI-llama-cpp
在 ComfyUI 中基于 llama.cpp 框架原生运行 LLM & VLM 模型。  
**[[📃English](./README.md)]**   

## 预览
![](./img/preview.jpg) 

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

## Text to Image Prompt 节点

该节点默认只执行透明的 LLM 调用：将你填写的 `system_prompt` 和
`user_prompt` 原样发给模型并返回结果，不会注入隐藏的分析、推理、规划、
自检或思维链 Prompt。

```text
System Prompt → User Prompt → llama.cpp → Prompt
```

- `Internal Prompt Engineering`：默认 `Disabled`，仅在主动开启后使用节点
  自带的简短图像 Prompt 优化指令（不含推理过程）。
- `Raw Mode`：开启后优先级最高，强制关闭内部增强，输入原样发送、模型内容
  原样返回。
- `Output Mode`：默认 `Raw`；`Text` 只清理首尾空白，`JSON` 只验证输出是
  有效 JSON；节点不会自动加入 Markdown、标题、编号或代码块。
- `Language`：默认 `Auto`，仅在内部增强开启时作为输出语言建议，不会触发
  隐藏的英文分析。

> **破坏性变更：** 旧版的 `subject`、`setting_words` 输入已替换为
> `system_prompt`、`user_prompt`。首次打开旧工作流时，请重新填写这两个
> 字段及新增选项。

## 更新日志

### 2026-07-30

- 将 `Text to Image Prompt` 节点由 `subject`/`setting_words` 扩写设计，
  替换为透明的 `system_prompt`/`user_prompt` 转发。**破坏性变更：**已有
  工作流需要重新填写这两个字段。
- 修复混合架构模型（如 Qwen3.5/3.6，及其他被 llama-cpp-python 判定为
  `is_hybrid` 的模型）在收到与上一次相同的 Prompt 时静默返回空字符串的
  问题。

### 2026-07-29

- 新增 `Text to Image Prompt` 文生图提示词节点。
- 改进 `mmproj` 兼容性。

## 致谢
- [llama-cpp-python](https://github.com/JamePeng/llama-cpp-python) @JamePeng  
- [ComfyUI-llama-cpp](https://github.com/kijai/ComfyUI-llama-cpp) @kijai
- [ComfyUI](https://github.com/comfyanonymous/ComfyUI) @comfyanonymous
