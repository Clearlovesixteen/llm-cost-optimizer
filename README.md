# LLM Cost Optimizer

用于审计 LLM API、Agent、MCP、RAG 和 AI 编程工作流中的 Token 浪费与端到端成本，并输出按收益排序的优化方案。

## 命令行安装

仓库当前为私有。先确保你的 GitHub 账号拥有仓库权限，并已配置 SSH，然后执行：

```bash
mkdir -p "$HOME/.agents/skills" \
  && git clone --depth 1 git@github.com:Clearlovesixteen/llm-cost-optimizer.git \
    "$HOME/.agents/skills/llm-cost-optimizer"
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force "$HOME\.agents\skills" | Out-Null
git clone --depth 1 git@github.com:Clearlovesixteen/llm-cost-optimizer.git "$HOME\.agents\skills\llm-cost-optimizer"
```

更新到最新版：

```bash
git -C "$HOME/.agents/skills/llm-cost-optimizer" pull --ff-only
```

最终应存在 `$HOME/.agents/skills/llm-cost-optimizer/SKILL.md`。Codex 通常会自动发现新 Skill；如果没有显示，重启 Codex。

如需让某个项目的所有成员自动发现它，也可以把仓库作为子模块放到项目的 `.agents/skills/llm-cost-optimizer/`。

## 调用

在 Codex 中输入：

```text
$llm-cost-optimizer 审计这个 Agent 项目的 Token 与端到端成本，先给方案，不改代码。
```

也可以这样使用：

```text
$llm-cost-optimizer 分析这些调用日志，找出重复上下文、缓存、工具载荷和重试问题。
```

```text
$llm-cost-optimizer 为这套 LLM 工作流设计成本监控口径和优化优先级。
```

## 默认边界

该 Skill 默认只做审计和优化建议，不会自动修改提示词、代码或配置。需要实际改造时，请在请求中明确说明允许修改的范围。

## 真实案例

仓库内附一份真实审计案例：在“读取一篇微信公众号文章并制作团队 Skill”的任务中，先后出现本地接口不可达、依赖缺失、网页直连失败，以及浏览器超时导致重复打开 4 个相同页面。最终通过复用已经打开的页面并只提取正文完成任务。

案例刻意不虚构 Token 或金额，而是依据可复核的调用记录指出：主要浪费来自失败空转、重复页面和工具路径选择，并给出可执行的路由、复用、熔断与埋点方案。详见 [`references/real-case.md`](references/real-case.md)。
