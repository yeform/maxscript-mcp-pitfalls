# maxscript-mcp-pitfalls

> 通过 MCP 驱动 3ds Max 写 MAXScript 建模时，**官方文档里查不到、只能靠踩坑发现**的实战避坑手册。
> 中文为主。53 条具体结论，来自 2026-11 三次 3ds Max 程序化建模会话（单日 12 版沙发、20+ 次语法重试）。

## 这是什么 / 为什么

用 AI Agent（经 MCP，如 [`cl0nazepamm/3dsmax-mcp`](https://github.com/cl0nazepamm/3dsmax-mcp)）在 3ds Max 里写 MAXScript 建模，
会遇到一整类「语法没错、文档没写、但就是不对」的坑：三角函数按**度**不是弧度、系统单位默认**英寸**、
`getOpenEdges` 的 `.count` 是最大索引不是个数、Arnold 类名带下划线、单剖面扫掠根本做不出扶手……

这些不是语法手册能覆盖的，而是**集成层 / 踩坑层**的经验。本项目把它们整理成一份可直接查阅的手册，
也整理成一个 Agent skill（`SKILL.md`）。

它**不重复**上游 `3dsmax-mcp` 自带的 MAXScript 语法参考，只补那之外的部分，二者配合使用。

## 内容（9 节 / 53 条）

| 节 | 覆盖 | 条目 |
|---|---|---|
| 一、纯语法陷阱 | 角度单位、`mod`、关键字、闭包、大小写、`for by -1`、`catch`… | 1–12 |
| 二、拓扑与网格 API | `getOpenEdges.numberset`、端面封口、ear clipping 绕序… | 13–22 |
| 三、系统单位与跨软件单位 | 英寸放大 25.4 倍、灯光 645 倍、Blender FBX 单位 | 23–25 |
| 四、Arnold 材质 | 类名下划线、渐变跑不通、分区材质方案 | 26–33 |
| 五、建模框架 | 扫掠做不出扶手、高靠背必然分件、先剪影后纹样 | 34–42 |
| 六、跨软件 / MCP 集成层 | 大图入上下文 413、`create_lights` 不支持 Arnold、`contact_check` 上限 | 43–50 |
| 七、效率方法 | 各环节耗时、三个提速做法 | 51–53 |
| 八、脚本自检清单 | 写完先过的 12 项 | — |
| 九、快速诊断表 | 症状 → 先查什么 | — |

完整正文见 [`SKILL.md`](SKILL.md)，逐条出处见 [`CHANGELOG.md`](CHANGELOG.md)。

## 怎么用

**方式 1｜当 Agent skill 用**：把 `SKILL.md` 放进你的 Agent skills 目录，例如
`~/.agents/skills/maxscript-integration-pitfalls/SKILL.md`，Agent 就会在写 MAXScript 时自动参考。

**方式 2｜当普通文档查**：直接读 `SKILL.md`，遇到症状查第九节「快速诊断表」。

## 致谢 / 依赖

- 配套上游项目：[`cl0nazepamm/3dsmax-mcp`](https://github.com/cl0nazepamm/3dsmax-mcp)（MIT）——
  本手册假定你已能通过它连接 3ds Max；其自带 MAXScript 语法参考（`maxscript-*.md`）与本文互补。
- 本文不包含上游任何文件，仅在正文中按其文件名引用。

## License

[MIT](LICENSE) © 2026 — 见 `LICENSE`。

---

## English (short)

A field-tested, Chinese-first handbook of **integration-layer pitfalls** for scripting Autodesk 3ds Max
via MAXScript over MCP — the kind of problems that aren't in the official docs and only surface after
repeated failures (trig functions take **degrees** not radians; default system units may be **inches**,
scaling everything 25.4×; `getOpenEdges.count` is the max index, not the count; Arnold class names carry
underscores; a single-profile sweep cannot make armrests, etc.).

53 concrete findings from three real procedural-modeling sessions (Nov 2026).
Complements [`cl0nazepamm/3dsmax-mcp`](https://github.com/cl0nazepamm/3dsmax-mcp) (MIT) — it does not
duplicate that project's bundled MAXScript syntax reference. See [`SKILL.md`](SKILL.md). MIT licensed.
