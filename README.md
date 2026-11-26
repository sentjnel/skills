# Mathematical Research Skills for Codex

面向数学研究与 LaTeX 证明工作流的 Codex skills 集合。

## Included skills

- `academic-math-writing`：撰写、修订和翻译基础数学论文、讲义与证明，附中文数学术语表。
- `plain-workflow`：以 Progress、Lemma、成熟结果归档和未决问题索引管理长期数学研究。
- `check-mathematical-proofs`：逐步审计证明的局部与整体正确性，检查精确目标、依赖、边界情形和冗余分支。
- `manage-manual-review-interventions`：管理人工审查意见、只读讨论、统一合并、版本冻结与交接。
- `iterate-proofs-from-reports`：独立核验完整审查报告，并据此直接迭代 LaTeX 证明稿、保留版本快照和验证结果。

## Repository layout

每个一级目录都是一个可独立使用的 skill 包，入口为 `SKILL.md`，可选的界面元数据位于 `agents/openai.yaml`。部分 skill 还包含其运行所需的 `references/` 文件。

## Installation

克隆或下载本仓库后，将所需的完整 skill 目录复制到个人 Codex skills 目录中。请保留每个目录的内部结构和文件名。
