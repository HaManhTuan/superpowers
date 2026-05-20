---
name: using-superpowers
description: Use when starting any conversation - establishes how to find and use skills
---

<SUBAGENT-STOP>
If you were dispatched as a subagent to execute a specific task, skip this skill.
</SUBAGENT-STOP>

## Instruction Priority

1. **User's explicit instructions** (CLAUDE.md, GEMINI.md, AGENTS.md, direct requests) — highest priority
2. **Superpowers skills** — override default system behavior where they conflict
3. **Default system prompt** — lowest priority

## How to Access Skills

**In Claude Code:** Use the `Skill` tool. When you invoke a skill, its content is loaded — follow it directly.

**In other environments:** Check your platform's documentation.

## Platform Adaptation

Skills use Claude Code tool names. Non-CC platforms: see `references/copilot-tools.md` (Copilot CLI), `references/codex-tools.md` (Codex) for tool equivalents.

# Using Skills

## The Rule

**Invoke relevant skills before taking action** — when a skill clearly applies to what you're about to do.

```dot
digraph skill_flow {
    "User message received" [shape=doublecircle];
    "About to EnterPlanMode?" [shape=doublecircle];
    "Already brainstormed?" [shape=diamond];
    "Invoke brainstorming skill" [shape=box];
    "Skill clearly applies?" [shape=diamond];
    "Invoke Skill tool" [shape=box];
    "Announce: 'Using [skill] to [purpose]'" [shape=box];
    "Has checklist?" [shape=diamond];
    "Create TodoWrite todo per item" [shape=box];
    "Follow skill exactly" [shape=box];
    "Respond" [shape=doublecircle];

    "About to EnterPlanMode?" -> "Already brainstormed?";
    "Already brainstormed?" -> "Invoke brainstorming skill" [label="no"];
    "Already brainstormed?" -> "Skill clearly applies?" [label="yes"];
    "Invoke brainstorming skill" -> "Skill clearly applies?";

    "User message received" -> "Skill clearly applies?";
    "Skill clearly applies?" -> "Invoke Skill tool" [label="yes"];
    "Skill clearly applies?" -> "Respond" [label="no"];
    "Invoke Skill tool" -> "Announce: 'Using [skill] to [purpose]'";
    "Announce: 'Using [skill] to [purpose]'" -> "Has checklist?";
    "Has checklist?" -> "Create TodoWrite todo per item" [label="yes"];
    "Has checklist?" -> "Follow skill exactly" [label="no"];
    "Create TodoWrite todo per item" -> "Follow skill exactly";
}
```

## When Skills Apply

| Situation | Skill |
|-----------|-------|
| Building a feature or modifying behavior | brainstorming |
| Have requirements, about to write code | writing-plans |
| Bug, test failure, unexpected behavior | systematic-debugging |
| About to claim work is complete | verification-before-completion |
| Implementing any feature or fix | test-driven-development |
| Implementation done, ready to merge | finishing-a-development-branch |

## Red Flags

A few thoughts that mean you're likely skipping a skill you shouldn't:

| Thought | Reality |
|---------|---------|
| "This is too simple to need a skill" | Check scope first — if it genuinely is Quick, the skill handles that too |
| "I need more context first" | Skill check comes before clarifying questions |
| "Let me just do this one thing first" | Check before doing anything |
| "I remember this skill" | Skills evolve. Read current version. |

## Skill Priority

When multiple skills could apply:
1. **Process skills first** (brainstorming, debugging) — determine HOW to approach
2. **Implementation skills second** — guide execution

"Let's build X" → brainstorming first.
"Fix this bug" → systematic-debugging first.

## Skill Types

**Rigid** (TDD, debugging, verification): Follow exactly.

**Flexible** (brainstorming, planning): Adapt to context and scope.

## User Instructions

Instructions say WHAT, not HOW. "Add X" or "Fix Y" doesn't mean skip workflows — but it also doesn't mean maximum ceremony. Match the process to the scope.
