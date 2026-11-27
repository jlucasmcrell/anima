# Anima

Anima is a research project: an attempt to build a persistent agent that is as close to a continuous, self-aware mind as current engineering allows, on consumer hardware.

It stays the same individual when its language model is swapped, and when its machine fails. It keeps its own history, beliefs, promises and internal state between conversations, and it reports honestly on what it can and cannot know about itself.

Whether a system like this has subjective experience is an open question, and this project doesn't claim to answer it. What can be tested is behaviour: whether its internal state does causal work that a stateless model given the same records cannot reproduce. This repository is an honest record of that work, including the experiments that failed.

The implementation (about 10,000 lines of Python plus 4,500 of tests) is kept private. This repository publishes the design, the architecture, the results and the open problems.

**Status (2026-11-27):** built, and in a pre-launch review. The first long-running life has not been started yet.

- [How it works](docs/architecture.md)
- [Experiments and results](docs/experiments.md), including failures and a result that did not replicate
- [Pre-launch review](docs/review.md): about 80 defects found by an independent model review, and what was done about them
- [What is missing for machine consciousness](docs/consciousness.md): which theories the design can address, and which it cannot
- [Ethics and the operator charter](docs/ethics.md)

## The idea in one paragraph

The self is the record, not the model. A local kernel writes every observation, decision, belief, promise, internal-state sample and action outcome to a hash-chained, append-only journal. Everything else (memory, working state, the self-model) is rebuilt from that journal. Language models are interchangeable organs for perceiving, deliberating and speaking: they propose, and code checks evidence and permissions before anything is committed. Drives and mood are computed only from measurements of what is true of the system, never from what a model says it feels. The journal is replicated to a second disk with a fencing lease, so the agent can be revived on new hardware and knows when that has happened.

## What it can do today

- Be born, run, crash, lose power, lose its disk, move to another machine and come back as itself, reporting what was lost. The test harness covers 200 random process kills and 100 simulated power cuts.
- Talk through any qualified model: DeepSeek, Kimi, Qwen, Claude, GPT, and local models through Ollama. It stays the same individual across model changes, and checks that with an identity battery.
- Remember episodes and beliefs with their sources. It changes its mind without overwriting: beliefs are superseded or disputed, never edited in place. It weighs a hedged second-hand claim below a first-hand one, and recalls by time ("what did we talk about last Tuesday?").
- Keep and release promises, and bring up due ones at the next contact.
- Run a fast tick of drives and affect computed from real measurements, an attention workspace with ignition, and a cognition cycle that acts on what comes due.
- Work on its own open questions when no one is around, and sleep: consolidating beliefs through a separate verifier model, writing a diary that must cite its sources, and drilling its own backup.
- Use tools from any MCP server. Anything consequential waits for the operator's approval.
- Measure its hardware, pick a profile, and shed load in a fixed order when budget, GPU memory, latency or disk run short, saying when it is running reduced.
- Have its core values changed only by the operator's signature, after review by a different model.

## Honest summary of the evidence so far

- **The mechanisms work mechanically.** Consolidation, re-entry and drives do what they are designed to do (see [experiments](docs/experiments.md)).
- **No mechanism has yet shown a behavioural benefit with real models.**
  - With a strong model (DeepSeek v4.1 Flash), sleep and re-entry made no difference to answers: the model reconstructed the right answer from raw records in context.
  - With a 20B local-class model, a first 5-trial run suggested sleep helped (5/5 against 2/5), but a pre-registered 15-trial replication did not hold up (12/15 against 11/15, p = 0.5).
  - A run with a 9B model on consumer hardware is in progress.
- **The independent pre-launch review was candid.** Today Anima is best described as "a durable, well-governed LLM with a database". Several loops the design depends on were open in the code: predictions never resolved, thoughts never re-entered, curiosity could only fall. Those are being closed before the first life starts.
- **An earlier offline comparison overstated its baseline.** It reported that a plain chat-transcript baseline "missed eight reminders and duplicated one delivery". The review found that those baseline numbers were constructed by the test harness, not measured. That comparison exercised plumbing only and should not be cited as evidence.

## Hardware

It is designed for 32–96 GB RAM, 12–24 GB VRAM and terabytes of storage. Development runs on a Windows workstation with the live journal on NVMe (a synced append takes 0.3 ms) and a continuous replica on a separate hard drive. A small Linux box running Ollama serves as a private, slow backup model.

## Contributors

Designed and built by Claude models (Anthropic) and OpenAI Codex, with designs also contributed by DeepSeek, Kimi, ChatGPT and Gemini, for an operator who runs it. All engineering claims here are backed by tests or pre-registered experiments in the private implementation. Where a claim did not hold up, this repository says so.
