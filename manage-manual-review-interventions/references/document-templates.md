# Opinion and handoff templates

Use these templates as structural checklists. Replace every placeholder with current evidence. Do not copy stale status, hashes, numbering, or version claims from an older project.

## Working opinion document

```markdown
# 《<document title>》<current version> 后续人工干预修改意见

当前主稿版本为 <version and date>。

<State whether prior opinions are merged and where their exact snapshot is archived.>

当前<无/有>待统一合并项。后续新增意见从“意见 <N>”继续编号。

## 意见 <N>：<concise decision title>

位置：<theorem, equation, paragraph, or stable text>

问题或决定：<agreed issue or instruction>

统一修改时：<exact required change, including formulas, domains, and quantifiers>

保持不变：<scope exclusions when needed>

覆盖关系：<optional; identify an earlier opinion superseded by this one>
```

For a definite simple correction, keep the item concise and literal. For a confirmed logical change, preserve the agreed reasoning and dependency implications needed to merge it safely.

After every append, update the introductory status so it states the actual pending range and the next opinion number. A header that still says “no pending items” while numbered opinions follow is invalid.

## Task handoff document

````markdown
# 《<document title>》<current version> 人工审阅交接

更新时间：<date and time if useful>

## 一、当前任务与权威入口

- 当前目标：<objective>
- 工作目录：<absolute path>
- 当前主文件：<path>
- 当前 PDF：<path>
- 当前意见文档：<path>
- 当前交接文档：<path>
- 当前版本：<version>
- 当前主文件哈希：<hash or not yet final>
- 当前 PDF 哈希：<hash or not yet final>
- 冻结目录：<paths that must not be edited>

## 二、开始时的完整阅读顺序

1. <handoff>
2. <opinion document>
3. <main manuscript>
4. <additional source or report only when required>

## 三、已经完成

1. <completed and verified item>
2. <completed and verified item>

## 四、尚未完成

1. <next concrete action>
2. <remaining validation or archive action>

## 五、已确认决定与覆盖关系

- <decision>
- <later opinion overriding earlier opinion>

## 六、来源与逻辑边界

- <verified source interface>
- <interface still open; do not overclaim>
- <independent derivation versus cited theorem>

## 七、文件变更与验证状态

- 已修改：<files>
- 保持只读：<files>
- 已运行：<commands/checks and results>
- 仍须运行：<final builds/text/render/hash checks>

## 八、继续工作的约束

1. <default read-only or currently authorized mutation scope>
2. <next opinion number>
3. <merge trigger and required order>
4. <formatting compatibility rule>
5. <do-not-edit archives or unrelated files>

## 九、可直接复制的新任务提示词

```text
<self-contained prompt from the template below>
```
````

## Copyable continuation prompt

Output this prompt on the page in a fenced `text` block. Do not use emphasis syntax inside it.

```text
请继续处理“<absolute working directory>”中的《<document title>》。

开始前请依次完整阅读：
1. “<handoff file>”；
2. “<opinion file>”；
3. “<main manuscript>”；
4. <additional report or source, only if required>。

当前任务状态：<version, completed work, pending opinions, and whether the main manuscript has been merged>。

默认权限：<read-only or exact authorized write scope>。当我以确定语气给出仅涉及局部符号或文字的简单修改时，直接写入当前意见文档，无需再次确认；逻辑、证明、组织或来源问题先讨论，待结论确认后再写入。

只有在我明确要求“统一合并”或“统一合并进 TeX”时，才修改主文档。统一合并时按以下顺序处理：先修改证明逻辑细节，再修改文章组织方式，最后统一符号记号；同一位置以靠后的意见为准。

不得改动：<frozen archives and unrelated files>。

最终验证要求：<two LaTeX builds, log, extracted text, all-page rendering, hashes, and version archive as applicable>。

页面回复暂不使用粗体或斜体；所有数学公式只使用行间形式。

下一步：<one exact action>。
```

## Handoff quality check

Before finishing the handoff, verify:

- the next agent can identify every authoritative file without guessing;
- completed and pending work are separated;
- no unfinished item is described as solved;
- exact restrictions and frozen paths are present;
- the next opinion number is current;
- source-verification boundaries remain honest;
- the copyable prompt matches the handoff rather than an older baseline;
- the prompt is visible in the user-facing response, not only stored on disk.
