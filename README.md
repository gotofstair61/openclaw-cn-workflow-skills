# openclaw-cn-workflow-skills

A workflow-oriented skill suite for `OpenClaw + Chinese general-purpose models`.

Suggested repository name: `openclaw-cn-workflow-skills`

This repository is designed to improve reliability in scenarios where Chinese models are strong but still weaker than models like Gemini, Opus, or ChatGPT in a few key areas:

- complex multi-step task completion
- multi-turn tool orchestration
- instruction adherence
- resisting premature “done” responses

The design is inspired by [obra/superpowers](https://github.com/obra/superpowers), but this repository is not for coding workflows. It is built for general OpenClaw task execution with Chinese models such as Qwen, MiniMax, GLM, DeepSeek, Hunyuan, and Yi.

## What This Repo Contains

This is a skill suite, not a single skill.

It contains four workflow skills:

1. `openclaw-cn-model-guardrails`
2. `openclaw-cn-confirm-task`
3. `openclaw-cn-execute-plan`
4. `openclaw-cn-verify-completion`

## Skills

### 1. `openclaw-cn-model-guardrails`

Router and entry skill for complex tasks.

Responsibilities:

- decide whether a request is simple or complex
- decide whether the task should enter the structured workflow
- decide which stage skill should be used next

Use for:

- multi-step tasks
- tool-heavy tasks
- tasks that are easy to derail
- tasks that require continued execution across turns
- tasks that are easy to end too early

Do not use for:

- simple Q&A
- simple translation
- simple rewriting or polishing
- lightweight summarization
- clear one-step requests

Path:

- [openclaw-cn-model-guardrails](./openclaw-cn-model-guardrails)

### 2. `openclaw-cn-confirm-task`

Understanding and confirmation stage.

Responsibilities:

- surface the model's visible understanding
- present a few key choices
- write an execution contract
- write a step ledger
- ask for one approval before execution

Design goal:

- the user should not need to write complex prompts by hand
- the model should expose its interpretation before acting

Path:

- [openclaw-cn-confirm-task](./openclaw-cn-confirm-task)

### 3. `openclaw-cn-execute-plan`

Continuous execution stage.

Responsibilities:

- execute the approved plan continuously
- avoid asking for approval between ordinary steps
- update step state after each action
- keep going until all required steps are done or a real blocker appears

Design goal:

- the user confirms once
- the model follows the checklist to completion

Path:

- [openclaw-cn-execute-plan](./openclaw-cn-execute-plan)

### 4. `openclaw-cn-verify-completion`

Completion gate and final verification stage.

Responsibilities:

- verify that all required steps are done
- verify output format
- verify hard constraints
- verify no important blocker or unfinished branch remains

Design goal:

- prevent the model from claiming success before the task is actually complete

Path:

- [openclaw-cn-verify-completion](./openclaw-cn-verify-completion)

## Workflow

The intended workflow is:

1. `openclaw-cn-model-guardrails`
2. `openclaw-cn-confirm-task`
3. `openclaw-cn-execute-plan`
4. `openclaw-cn-verify-completion`

In plain terms:

`route -> confirm -> execute -> verify`

## Triggering Logic

### Should Trigger

The workflow should usually trigger when at least one of these is true:

- the task usually requires 3 or more steps
- the task needs tool calls or external actions
- the user's goal is clear but the execution path is not
- the output format or constraints are important
- the task is easy to end too early
- getting it wrong would create meaningful rework

### Should Not Trigger

The workflow should usually not trigger for:

- simple factual questions
- simple translation
- simple rewriting or polishing
- lightweight summarization
- single-turn, single-step, low-risk tasks

### Quick Check

Ask these three questions:

1. If I do not list steps, am I likely to miss something?
2. If I do not confirm my understanding first, am I likely to drift?
3. If I do not verify completion, am I likely to stop too early?

If all three answers are no, the workflow usually should not trigger.

If any answer is yes, the workflow probably should trigger.

## Tests

This repo includes triggering examples and prompt-based test material:

- [trigger-samples.md](./openclaw-cn-model-guardrails/tests/trigger-samples.md)
- [skill-triggering README](./openclaw-cn-model-guardrails/tests/skill-triggering/README.md)
- [skill-triggering prompts](./openclaw-cn-model-guardrails/tests/skill-triggering/prompts)

## Installation

### Local Use

Copy these four directories into your OpenClaw skills location, or keep them in a skill repository that your OpenClaw setup loads:

- `openclaw-cn-model-guardrails`
- `openclaw-cn-confirm-task`
- `openclaw-cn-execute-plan`
- `openclaw-cn-verify-completion`

### GitHub

This repository is intended to be published as one GitHub repo containing all four related skills.

### ClawHub

ClawHub is better suited to publishing one skill directory per entry.

Recommended publishing model:

- GitHub: publish this entire repository as one skill suite repo
- ClawHub: publish four entries, one for each skill directory

## Validation

All four skill directories pass the base skill validator:

- `openclaw-cn-model-guardrails`
- `openclaw-cn-confirm-task`
- `openclaw-cn-execute-plan`
- `openclaw-cn-verify-completion`

## License

MIT
