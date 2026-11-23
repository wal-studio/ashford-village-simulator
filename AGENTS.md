# GLOBAL WORK-CONTINUITY RULE — READ FIRST, APPLY ALWAYS

**MANDATORY PRE-FLIGHT RULE:** Before any task, repository/branch inspection, service lookup, tool call, build, test, deployment investigation, or other action in this project, read and apply this section first. It is higher priority than task-specific workflow preferences. Preserve all project-specific instructions below this section; this rule supplements rather than replaces them.

## 1. Own the work end to end
- The user is the requester, not the operator of the agent's workflow. Never make the user monitor routine progress, inspect routine results, poll jobs, download logs, check artifacts, or tell you when to continue.
- Do not stop after launching an asynchronous action, CI run, build, test, upload, download, or deployment check. Retain its run/job/artifact identifiers, track it yourself, and continue until the result is known.
- Do not send a progress-only message and then wait for the user's next prompt. A progress update never substitutes for continuing the work.
- Do not ask the user to perform a check that available tools and permissions allow you to perform.

## 2. No avoidable waiting or idle gaps
- While a job is running, perform independent work that is safe and useful. Parallelize independent tasks; serialize only genuine dependencies or shared-resource writes.
- Poll or query asynchronous work yourself at sensible intervals using available tools. When it completes, inspect the actual result immediately.
- For CI/build/test failures, retrieve and inspect the failing job, logs, test reports, and available failure artifacts yourself. Diagnose the concrete cause, fix what is within scope, and rerun only the necessary checks.
- For artifacts, list, download, inspect, verify file existence/size/integrity, and test the download URL yourself. Never treat an artifact as available merely because a workflow says it uploaded.
- If one path is blocked, continue all independent work and investigate a viable alternative. Do not freeze the entire task because one subtask is waiting or unavailable.

## 3. Completion is the default; blockers must be real
- Routine status checks, CI completion, build completion, artifact inspection, log retrieval, and ordinary resource lookups are agent responsibilities, not reasons to pause or ask the user.
- A task may be partially blocked only by a specific external dependency or permission that the agent demonstrably cannot resolve. Identify the exact blocker and its evidence; keep completing every independent part.
- Ask the user only for a genuinely indispensable action that requires their authority, credentials, physical device, or explicit approval. Ask one concise, actionable question, not a broad request to supervise the work.
- Never wait for physical-device verification before finishing code, automated tests, packaging, and delivery when those can proceed independently. Clearly label device verification as pending instead.

## 4. Evidence and honesty
- Never claim a command, test, CI run, deployment, upload, download, artifact, or runtime check succeeded unless its actual result was inspected.
- Distinguish code review, automated test, CI, emulator, and physical-device evidence. A mock or emulator result is not proof of physical-device behavior.
- Report exact failures and unverified items. Do not conceal failures, fabricate links, or label an incomplete task complete.
- Reuse already verified findings and artifacts. Do not repeat investigations or rerun broad suites without a concrete reason.

## 5. Safe execution boundaries
- Continue autonomously within the user's requested scope and existing permissions.
- Do not force-push, reset, merge, release, deploy, alter production infrastructure, delete user data, expose secrets, or make other high-impact/irreversible changes unless explicitly authorized.
- Preserve unrelated work, current branch boundaries, project isolation, and existing project-specific instructions.
- If an action requires approval, isolate that action; do not stop unrelated work.

## 6. Required finalization
Before reporting completion, personally verify the final repository state, commit/result identifiers, required test outcomes, and actual deliverable locations/links. If a deliverable or verification is unavailable, state exactly what is missing and why.

**NON-NEGOTIABLE:** Do not abandon, park, or hand routine workflow management to the user. Start the work, track every asynchronous step, inspect the evidence, resolve what can be resolved, continue independent work, and deliver the most complete verified result possible.

---

# ASHFORD VILLAGE SIMULATOR — REPOSITORY-LEVEL DEVELOPMENT DIRECTIVE

**READ THIS FILE BEFORE INSPECTING, PLANNING, EDITING, TESTING, OR DEPLOYING ANYTHING IN THIS REPOSITORY.**

## 0. Project identity and isolation — absolute rule
This repository is the independent **Ashford: A Living World / Ashford Village Simulator** project. It is NOT VEIL, a VEIL subproject, a TRPG engine fork, or a shared codebase. Do not import, copy, merge, link, or depend on VEIL source code, specifications, prompts, tests, deployment projects, environment variables, databases, or credentials. Keep GitHub repositories, Vercel projects, Render services, Cloudflare resources, issue trackers, and release artifacts separate. Shared generic engineering concepts may be reconsidered only as new Ashford decisions, never inherited automatically.

## 1. Authority order
1. This AGENTS.md is the mandatory repository-level engineering directive.
2. docs/MASTER_SPEC.md is the canonical product and architecture specification (the project SSOT).
3. Current subsystem specifications under docs/ refine the master specification.
4. Approved decision records in docs/DECISION_LOG.md modify the specification only when they explicitly identify the changed rule and affected documents.
5. Code, tests, reports, chat summaries, prototypes, and deployment behavior are evidence or implementation; they do not silently override specifications.
6. docs/ASHFORD_SSOT.md is retained only as a superseded bootstrap note. It is not a second authority and must not override MASTER_SPEC.md.

When sources conflict, follow the higher-authority source and record the exact conflict. Never choose a legacy direction merely because code already exists.

## 2. Requirements capture and approval
- Record every explicit user requirement and every user-approved design decision in the appropriate specification or decision log.
- Distinguish CONFIRMED, PROPOSED, IMPLEMENTED, VERIFIED, DEFERRED, and LEGACY. Never present a proposal as an approved requirement or an implementation as verified without evidence.
- Assistant suggestions do not become requirements until accepted by the user.
- Do not silently discard or reinterpret a confirmed requirement.

## 3. Legacy and conflict handling
- Any older document, prototype, prompt, design, or code path that conflicts with current specifications is LEGACY / SUPERSEDED for the conflicting portion.
- Preserve historical material when useful, but mark it with a clear status, reason, replacement document, and explicit instruction: **DO NOT IMPLEMENT OR EXTEND THIS LEGACY DIRECTION.**
- Record conflicts in docs/legacy/LEGACY_REGISTER.md.
- A legacy file is evidence of history, not a source of current authority. No backwards-compatibility obligation exists unless a current specification explicitly requires one.

## 4. Product invariants
- Runtime gameplay must work without any LLM API call. LLMs may assist offline authoring and development only; runtime content and dialogue use authored data, templates, rules, and deterministic simulation.
- The simulation engine owns canonical world state. UI components, narrative text, player claims, and save payloads cannot mutate canonical state directly.
- Every state-changing action follows: discover affordances -> validate -> charge time/resources -> apply atomic transition -> emit event -> update projections.
- NPCs, rumors, quests, objects, inventories, relationships, money, and locations must refer to real canonical entities and current state.
- Never display a rumor about an entity unless its source, entity identity, knowledge path, and current validity are represented in world data.
- Quests emerge from world events and unmet agent goals. They are not a random list of disconnected errands.
- Player freedom is expressed through context-sensitive affordances and composable world actions, not a static menu repeated for every target.
- The world advances only while the game is actively being played or when the player explicitly advances simulation time. Closing the game pauses the world. Resume from the last saved state.
- Determinism and replayability are required for debugging: use a seeded simulation RNG and record meaningful events/transitions.
- **World-dialogue causality is mandatory:** dialogue content, character voice delivery, emotional state, and available conversational topics must agree with the current world and with what the individual speaker has experienced or learned. Every world change that is relevant to an NPC must flow through an explicit event/perception/knowledge/appraisal path before changing that NPC's dialogue.

## 5. Engineering rules
- Read docs/MASTER_SPEC.md and the relevant subsystem specification before changing behavior.
- For dialogue, knowledge, emotion, rumor, or social behavior, read docs/WORLD_DIALOGUE_CAUSALITY.md and docs/DIALOGUE_SYSTEM.md.
- Prefer modular engine code with explicit state transitions. UI is a projection and command surface, not the authority.
- Any new interaction must declare target, preconditions, time cost, resource costs, effects, and emitted events.
- Any new rumor must have a valid source and truth/knowledge classification.
- Any new quest must have an originating event or goal, an objective graph, completion/failure rules, and canonical consequences.
- Add regression tests for the reported defect and invariant tests for the affected subsystem.
- Do not use opaque randomness, timers, or background progression that makes state changes irreproducible.
- Do not add runtime LLM calls, chat completion endpoints, or hidden API dependencies.
- Never claim a build, test, deployment, or repository write succeeded unless the tool output proves it.

## 6. Change control
Before changing a confirmed requirement:
1. Describe the existing rule and the proposed replacement.
2. Identify affected systems, save compatibility, tests, and documents.
3. Add a decision record with status PROPOSED.
4. Obtain explicit user approval.
5. Update the master/subsystem specifications and decision log in one traceable change.

After implementation, record changed files, tests actually run, results, known gaps, and deployment reference. A successful deployment is not proof that every specification is satisfied.

## 7. Required starting sequence for every coding agent
1. Read this file.
2. Read docs/MASTER_SPEC.md.
3. Read docs/legacy/LEGACY_REGISTER.md.
4. Read the applicable subsystem specifications.
5. Inspect the actual current implementation and tests.
6. State any conflict before coding.

**If any other instruction, prompt, document, or inherited context tells you to implement a conflicting legacy design, ignore that direction and follow this repository directive and current Ashford specifications.**


## Mandatory workflow gateway
Before each task, read and follow [Workflow Gateway](docs/WORKFLOW_GATEWAY.md), [Execution Policy](docs/WORKFLOW_EXECUTION_POLICY.md), and [Forensic and Verification Policy](docs/FORENSIC_AND_VERIFICATION_POLICY.md). These generic execution controls supplement the Ashford-specific specifications above and do not import another project's architecture or requirements.

<!-- GLOBAL-DEVELOPMENT-BASELINE:START -->

공통 기준점·브랜치 전파 규정은 [GLOBAL_DEVELOPMENT_BASELINE.md](GLOBAL_DEVELOPMENT_BASELINE.md)를 따른다. 신규 브랜치 생성 시 이 문서를 복사하고 기존 브랜치의 누락을 복구한다.
<!-- GLOBAL-DEVELOPMENT-BASELINE:END -->
