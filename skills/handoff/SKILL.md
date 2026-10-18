---
name: handoff
description: Write a handoff document so a fresh agent can pick up the current work. Use when the user asks for a handoff, to hand off work, or to compact the session into instructions for another agent.
disable-model-invocation: true
---

# Handoff

Compact the current session into a handoff document that a fresh agent (with
none of this context) can pick up and continue from. The agent may be on an entirely different
harness. Do not reference task IDs, sub-agents, or other artifacts of this session.

## Rules

- Write the document **from current context only**. Once handoff is requested,
  make no further tool calls except the single write of the document itself.
  Do not re-read files, re-run commands, or gather new information.
- Write the document to the temporary directory, e.g.
  `/tmp/handoff-<topic>-<YYYYMMDD-HHMM>.md`.
- After writing, report to the user a concise summary of the handoff document
  and its full path. Nothing else.

## Document contents

Write for an agent that knows the repo conventions (AGENTS.md) but nothing
about this session. Include:

- **Goal**: what the user ultimately wants, in their words where possible.
- **State**: what has been done and verified so far, including files changed
  and commits made.
- **Remaining work**: concrete next steps, in order, with enough detail to act
  without rediscovery.
- **Key knowledge**: load-bearing facts learned this session — file paths,
  function names, data findings, failed approaches and why they failed,
  user decisions and preferences stated during the session.
- **Verification**: how to check the work (commands, queries, expected
  output).

Omit sections that are empty. Prefer specific paths, names, and numbers over
prose summaries; the reader cannot see this conversation.
