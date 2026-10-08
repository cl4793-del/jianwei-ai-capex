# 项目文件格式

普通用户无需写 JSON：页面的「下载项目文件」会生成合法文件，可在同一工具导入。开发者可参考 `examples/blank-project.json` 和 `examples/ai-capex.json`。

顶层 `version` 必须是数字 `1`。`title` 与 `question` 必填；`description`、`hypothesis`、`asOf` 和 `conclusion` 为文字。`sources`、`claims`、`evidence`、`stages` 均为数组，每类最多 200 项。每个记录的 `id` 为同类内唯一的非空字符串；关联资料使用 `sources` 数组，编号必须存在于顶层资料库。

| 数组 | 记录字段 |
| --- | --- |
| sources | id、title、kind、meta、url、body、boundary；title 与 body 必填 |
| claims | id、title、type、text、question、sources；title 与 text 必填 |
| evidence | id、title、stance、text、sources；stance 为 support 或 challenge，title 与 text 必填 |
| stages | id、title、date、text、change、sources；title 与 text 必填 |

链接仅接受完整 http / https 地址或空值。文本字段显示为纯文字，不能嵌入 HTML。文件最大 2 MB，每个普通文字字段最多 20,000 字符，结论最多 50,000 字符。导入前检查格式及资料引用，失败时保留原项目。未知字段会被忽略。

空白模板不携带资料或预置判断。AI 案例的静态补充表位于 `dist/index.html`，只有项目保留原 Alphabet 来源时才显示；它不是 JSON 中可编辑的通用表格。要更换初始示例，在 `dist/research-data.js` 中替换 `exampleProject`，使用同一格式。已有浏览器保存内容优先于默认示例。
