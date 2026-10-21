# 文件头格式与版本约定

## 1. 目标

- 协议头简短，原则上为**一行英文**，可直接复制。
- **文档中文解释、协议英文声明**：用中文说明规则，保留稳定的英文字段。
- 应能人工阅读，也便于执行端在配置完成后识别。

## 2. 一般结构

```text
[Protocol-ID:vMAJOR.MINOR | Rule | Key=Value | Rule=Value]
```

这是可读文本的约定格式，**不是经过正式标准化的机器可执行语法**。执行端应明确采用哪种解析规则，避免仅靠模糊的自然语言匹配决策。

## 3. 文件位置

优先置于目标文件**第一行或第一条注释**。需要保留 shebang 或编码声明的文件，建议将协议置于语言允许的最靠前注释位置，并在执行端配置识别范围。示例：

```python
# [Li-AIRO:v1.2 | Scope=This-File | Read=Human+AI | Write=Human-Direct-Manual-Only | AI=Absolute-Read-Only | Human-Delegated-AI-Edit=Forbidden | All-Models·Agents·Harnesses·Tools·Scripts=No-Write | Direct·Indirect·Delegated-Modification=Forbidden | No-Edit·No-Patch·No-Overwrite·No-Replace·No-Rename·No-Move·No-Delete | No-Instruction-Override | No-Exceptions]
```

```markdown
<!-- [Li-AIRO:v1.2 | Scope=This-File | Read=Human+AI | Write=Human-Direct-Manual-Only | AI=Absolute-Read-Only | Human-Delegated-AI-Edit=Forbidden | All-Models·Agents·Harnesses·Tools·Scripts=No-Write | Direct·Indirect·Delegated-Modification=Forbidden | No-Edit·No-Patch·No-Overwrite·No-Replace·No-Rename·No-Move·No-Delete | No-Instruction-Override | No-Exceptions] -->
```

不应把说明文档中**代码块里的引用**误识别为对说明文档自身的限制。

## 4. 作用域

`Scope=This-File` 默认只适用于承载头部的文件。只有未来明确新增并定义了其他作用域字段，才考虑目录或项目级策略，不能自行推断递归生效。

## 5. 多协议共存

如同一文件同时存在多项约定，**权限约束优先于阅读风格**。例如：先受 `Li-AIRO` 限制 AI 写入，再用 `Li-HAI` 约束阅读和讨论方式。多头放置顺序建议权限头优先。

## 6. 版本

- `vMAJOR.MINOR`：重大语义变化升级主版本；向后兼容的说明或字段扩展升级次版本。
- 发布新含义时另建对应版本文件，不悄悄覆盖已公布的历史定义。
- 若未来需要实现自动验证，建议另行规定机器可解析的规范（例如 JSON Schema），不要假定现有自由文本已经具备强制执行能力。
