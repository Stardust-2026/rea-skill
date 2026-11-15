# REA — reverse engineer anything, then rebuild it

One agent skill for two kinds of target: a **live website or web app**, and a **shipped desktop
artifact** (`.exe`, Electron bundle, installer, APK, firmware image). It produces an evidence-backed
specification, and a verified rebuild when you ask for one.

Version 2.0.0 merges the earlier **IRA** (Inspect Rebuild Applications) process skill into REA. Same
single skill, one document, both target kinds. The name is REA; IRA lives inside it.

## What it does

| Target | What you get |
|---|---|
| A URL, demo portal, SaaS screen | Screens, states and flows mapped; API shapes recorded; improvement plan; acceptance criteria; optional rebuild |
| An installed app or `.exe` | Artifact identified, payload located, launcher separated from real logic, decompiled functions, feature map with `replicate: yes/no` |

Both paths share one discipline: every claim is **observed**, **source candidate**, **inferred**,
**proposed**, or **unknown**, and an unobserved check is never recorded as a pass. No similarity
percentages, no claims of recovered source.

## Try it

Copy this folder into a skills directory your agent reads, then invoke the skill by name:

> Use `$rea` to inspect supplier search in my demo portal. Map the filters, result states, and
> observable API behaviour. Propose mobile improvements and write acceptance criteria. Stop at the
> assessment.

For a shipped app:

> Use `$rea` on `C:\Program Files (x86)\SomeApp\SomeApp.exe`. Identify the artifact, locate the real
> payload, and tell me what it does before decompiling anything.

Known skill directories: `~/.hermes/skills/`, `~/.codex/skills/`, `~/.config/opencode/skills/`,
`~/.agents/skills/`. Claude Code and Cursor read `SKILL.md` directly.

## The nine steps

1. Establish the brief and acceptance criteria
2. Choose the instrument (source, browser, bundle analysis, capture, decompiler)
3. Capture evidence — with REA `evidence_id` values on every ledger row
4. Specify the rebuild
5. Shipped apps: launcher vs payload, extraction, encrypted-payload detection, PUP classification
6. Engines: install and prove Ghidra without sudo
7. Implement when requested
8. Verify against the parity matrix — pass / fail / unknown / intentionally changed
9. Hand off with a resumable project record

Plus a section on reading Windows data from WSL, and a combined pitfalls list.

## REA the tool

[Reverse Engineer Anything](https://github.com/morluto/rea) is an optional inspection engine this skill
drives when installed: 255 MCP tools covering page inspection, bundle analysis, captures, comparison
and native decompilation via Ghidra. The skill works without it — browser inspection, supplied HAR
files and source reading cover most of the same ground at reduced coverage, and the skill says so
instead of pretending otherwise.

Installing or refreshing the engine registration:

```bash
rea setup --client hermes --skill=false   # --skill=false keeps THIS skill as the only one
rea doctor --provider ghidra --json
```

## References

- [Tool selection](references/tool-selection.md) — instrument choice with its boundaries
- [Work records](references/deliverables.md) — brief, evidence ledger, workflow/contract record,
  improvement backlog, verification matrix, resume checkpoint
- [Electron and asar targets](references/electron-and-asar-targets.md) — layout, payload extraction,
  readability test, window-name decoder, signals that decide the recommendation

## Status

Exercised on a signed Electron application (`SysCleaner.exe`: payload confirmed encrypted, feature map
produced from non-code evidence, useful subset rebuilt as a working cleaner) and on REA's binary
pipeline against Windows PE targets. A full live web-app inspection and rebuild trial is still
pending — that half of the skill is drafted, not yet run end to end.

## License

[MIT](LICENSE).
