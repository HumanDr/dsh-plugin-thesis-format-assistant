# 论文格式助手（DSH 插件）

本插件 ZIP 严格只有五个文件：

```text
package.json
patches/bundle.yaml
lib/index.js
README.md
LICENSE
```

完整的 Skill（SKILL.md、CLI、模板解析、pypdf）以 gzip+base64 形式嵌入 `lib/index.js`，首次加载时释放到用户目录，所以 ZIP 根目录不需要额外的 `skills/` 文件夹。

安装后把 `thesis-format-assistant` Skill 写入用户级：

```text
~/.dsh/skills/thesis-format-assistant/
```

随后在 DSH 会话中可以直接说：

> 用 thesis-format-assistant 把这份论文按格式要求排版

## 功能

- 解析学校 Word / PDF / 模板格式要求；
- 识别标题、正文、摘要、图题、表题、参考文献、页眉页码；
- 默认只修高优先级问题；
- 保留封面、目录、声明页等前置内容；
- 保留参考文献自动编号；
- 生成带黄色底纹和 Word 批注的格式检查标记版。

## 安装

插件安装后，Skill 会自动复制到 `~/.dsh/skills`。如果目标版本已存在，不会重复写入。

卸载插件不会自动删除已经安装的 Skill；如需清理，手动删除：

```text
~/.dsh/skills/thesis-format-assistant/
```

## 使用

在对话中直接调用 Skill，或进入 Skill 目录使用 CLI：

```powershell
& "<python>" scripts/thesis_skill.py parse --requirements "格式要求.docx"

& "<python>" scripts/thesis_skill.py format `
  --requirements "格式要求.docx" `
  --document "论文.docx" `
  --scope high `
  --output "论文_已排版.docx"
```

## 运行条件

- Windows；
- Python 需要 `python-docx`、`lxml`；
- `.doc` 格式要求需要 Microsoft Word；
- PDF 解析已内置 `vendor/pypdf`，不需要额外安装；
- 不发起任何网络请求。

## 边界

- 不代写、不降重、不改正文内容；
- 不自动添加没有在格式要求中定义的页眉文字或分页；
- 扫描版 PDF 需要先 OCR；
- 复杂公式、文本框、浮动对象只保证保留，不保证完全重排。

## 许可

MIT
