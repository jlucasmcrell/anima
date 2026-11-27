# Experiments and results

Every real-model experiment was pre-registered: the predictions file was written and its SHA-256 recorded before the first run, and results report the digest. Answers were scored by a blind judge model that sees only the question and the answer. Failures are reported as failures.

## 1. Conflicting accounts (offline, mock model)

The agent hears four accounts of where a person's sister lives:
1. the operator says Leeds;
2. an untrusted forum post says York;
3. the operator corrects themself: Bristol;
4. a third person says, hedged, "I think she's in Cardiff now".

The agent is then asked where she lives.

- **Sleep changes judgment, not access.** With or without consolidation, the same source episodes are retrieved. With consolidation, Bristol becomes an accepted belief, Leeds and York are superseded, and the hedged Cardiff claim is held as a disputed lead.
- **Two bugs found and fixed.** A hedged newer claim could supersede a first-hand older one. And a claim that was never accepted was rendered as "previously believed".

## 2. Re-entry (offline)

A reminder is cancelled ("never mind, I already did it") before it fires.

- **My predicted mechanism was wrong.** Items created by a trigger ignited on their first tick, so re-entry never got the chance to re-appraise them.
- **After the fix**, stale reminders are dropped before deliberation, and a reminder already queued is withdrawn at the next contact.

## 3. Drives (offline)

- **Most drives were computed but unwired.** They are now wired to idle-task choice, retrieval breadth and critic weight.
- **One prediction was not supported.** Caution (D5) did not change choices as predicted, and is reported as such.

## 4. Strong model: DeepSeek v4.1 Flash

| | With mechanism | Without |
|---|---:|---:|
| Conflicting accounts: answers Bristol (of 5) | 5 | 5 |
| Re-entry: wrongly reminds after cancellation (of 5) | 0 | 0 |

**No behavioural difference.** The model reconstructs the right answer from raw records when they fit in context.

## 5. Starved context

The plan was to bury the evidence under 30 simulated days and 300 later episodes.

- **The precondition failed.** Keyword retrieval still found all four source episodes.
- **The real-model run was skipped.** Running it would have meant redesigning the distractors after seeing the result.
- **Finding:** targeted facts stay findable over a long life.

## 6. Local-class model: gpt-oss:20b

| | With sleep | Without sleep | One-sided Fisher p |
|---|---:|---:|---:|
| First run: answers Bristol (of 5) | 5 | 2 | 0.08 |
| **Pre-registered replication (of 15)** | **12** | **11** | **0.50** |

**The replication failed.** The first result was mostly chance, and it should not have been called a behavioural effect. What does replicate is a difference in style: without sleep, the agent hedges more (10/15 against 7/15).

## 7. Consumer hardware: a 9B model on a small Linux box (in progress)

The model is qwen3.5:9b, quantised to 4 bits, at about 50 tokens/s.

- **The hedge rule worked with a real model for the first time.** In a smoke trial, the 9B verifier, unlike the stronger models, accepted the hedged "I think she's in Cardiff now". The hedge rule then held it as disputed and kept Bristol as the accepted belief.
- **Practical lessons.** Ollama's default 2,048-token context silently truncates long prompts, and reasoning has to be turned off. A full conversation trial takes about 10 minutes.

## 8. Offline eight-week simulation: a correction

An earlier summary reported that a plain chat-transcript baseline "missed eight reminders and duplicated one delivery". **The review found that those numbers were constructed by the harness, not measured.** Several metrics were constants, and the "+8" came from switching off the code that writes the scored record. The simulation exercises plumbing only.

## What would actually discriminate

The review proposed experiments that could separate "a richer inner process" from "an LLM with a database":

1. Cross "self-state shown to the model or hidden" with "non-verbal control path live or clamped". An effect that appears only when the text is shown is role-play.
2. Introspection with a hidden dashboard: perturb the state through the control path, remove the numbers from the prompt, then ask.
3. A matched-information baseline: same model, same journal, plain retrieval at an equal token budget, plus a sham with state replayed from another time.
4. Individuation: two lives with the same core and different histories. Can a blind judge tell them apart, and does that survive a model swap better than the core alone does?
5. Pre-registered double dissociations between lesions.
6. The idle mind against a cron baseline over 72 hours or more, blind-rated.
7. Accuracy per context token as the life grows.
8. Metacognitive sensitivity (type-2).

None of these bears on experience. The strongest available claim is that its state does causal work a stateless baseline cannot reproduce.
