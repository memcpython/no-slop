<p align="center">
  <img src="assets/no-slop.gif" alt="NO SLOP. An animated four-step workflow: read the code, trace the root cause, make the right change, and verify the result." width="100%">
</p>

<h1 align="center">no-slop</h1>
<p align="center"><strong>Stop shipping code that only looks correct.</strong></p>
<p align="center">
  <a href="#the-point">The point</a> ·
  <a href="#the-rules">The rules</a> ·
  <a href="#install">Install</a> ·
  <a href="SKILL.md">Read the skill</a>
</p>

---

## The point

AI can write a hundred lines before understanding the first one.

It can invent APIs, bury bugs under fallback logic, rewrite working code because reading it takes effort, and then tell you the implementation is *production-ready*.

**`no-slop` pushes back against that.**

One `SKILL.md`. No runtime. No dependencies. Just a set of rules for agents that write, debug, refactor, or review code.

**Think first. Change less. Prove what works.**

## The rules

| No more | Do this instead |
| :--- | :--- |
| Guessing how an API works | Check the installed version and actual contract |
| Patching symptoms | Trace the failure to its cause |
| Rewriting working code for convenience | Make the smallest coherent change |
| `try/catch` everywhere | Handle errors where recovery makes sense |
| Comments that narrate the obvious | Explain only what the code cannot |
| Random managers, wrappers, and factories | Add abstractions only when they earn their keep |
| “Fixed” without a test or reproduction | Say exactly what was verified |

The skill also requires checking callers, preserving behavior, distinguishing evidence from assumptions, and reporting uncertainty instead of bluffing.

## Install

Download [`SKILL.md`](SKILL.md) and place it in your agent's skills directory:

| Agent | Project-local | User-wide |
| :--- | :--- | :--- |
| **Codex** | `.agents/skills/no-slop/SKILL.md` | `~/.agents/skills/no-slop/SKILL.md` |
| **Claude Code** | `.claude/skills/no-slop/SKILL.md` | `~/.claude/skills/no-slop/SKILL.md` |

Or install it into any agent that supports the [Agent Skills format](https://agentskills.io/).

Start a new agent session after installing. If your agent doesn't load the skill automatically, invoke `no-slop` explicitly in your coding request.

<details>
<summary><strong>Example: what changes in practice?</strong></summary>

Instead of:

```python
def get_name(user):
    try:
        return user.name
    except Exception:
        return "unknown"
```

The agent should first establish whether `user.name` is guaranteed by the actual contract. If it is:

```python
def get_name(user):
    return user.name
```

If missing names are valid, handle that *specific* case. Swallowing every exception isn't robustness; it hides failures.

The real task is understanding the contract, not making the code shorter.

</details>

## What this is / isn't

**It is:** an instruction-only skill that encourages careful investigation, focused changes, useful comments, and evidence-backed verification.

**It isn't:** a linter, a security scanner, a code-quality benchmark, or a guarantee that a model will follow every instruction. Results depend on the agent, project, and task.

The entire skill lives in **[`SKILL.md`](SKILL.md)**. Read it, fork it, change what you disagree with.

---

<sub>MIT licensed. See <a href="LICENSE">LICENSE</a>.</sub>
