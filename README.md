# Anima

Anima is a research project exploring persistent identity and cognition in an agent that can change language models and recover on different hardware. Its observable behavior can be tested. Whether such a system has subjective experience remains an open question.

## Design

A local kernel records observations, decisions, commitments, and action outcomes in a durable journal. Memory and working state can be rebuilt from that history. Models propose interpretations and actions. The kernel checks evidence and permissions before committing a change. A scheduler tracks attention and unfinished commitments between conversations. During idle periods the agent reviews experiences and consolidates memory.

On restart the agent verifies its history, reconciles interrupted actions, and reports gaps in its observations. Hardware and token budgets determine which model roles and background tasks can run.

## Milestones

| Stage | Implementation history |
| --- | --- |
| Foundation | Journal, recovery, replica fencing, encrypted archives, and model routing implemented. |
| Memory and cognition | Sourced beliefs, commitments, attention, measured drives, identity checks, and sleep consolidation implemented. |
| Tools and hardware | Tool approvals, hardware profiling, and a resource degradation ladder implemented. |
| Hardening | Under development. The first milestone targets verified journal startup with 300,000 records and bounded index memory. |

This repository publishes the design outline and milestone history. The implementation is maintained separately.

### Verified journal indexes

The implementation now checks sealed journal segments and reads older record headers on demand. On the development machine, a fresh open of 300,000 synthetic records took 0.739 seconds. A separate allocation measurement retained 9.4 bytes per record. These figures cover the journal. The implementation suite passed 133 offline tests, including recovery from interruptions during index and seal publication.

### Resource pressure and recovery

The agent can reduce the number of options it considers, prefer a cheaper qualified model, defer diary writing, and slow its tick under resource pressure. An offline test observed the cheaper model taking over and the original model returning as the pressure eased. The implementation suite passed 134 tests.

### Memory rehearsal

Time since recall, spaced repetition, importance, and measured arousal now influence which memories surface. Sleep can preserve a verified excerpt from a fading memory, with a reference back to its source. Tests verified ranking, replay, and resumption. All 135 offline tests passed, including the extended crash suite.

### Drift and character

Weekly reviews compare recent behavior with available historical evidence and flag unexplained changes. Character revisions require supporting examples on three distinct nights. The agent can reconstruct its signed character file from its journal. Simulations exercised a month of reviews and a comparison window 90 days in the past.

### Learning from tool outcomes

Three successful similar requests can establish a provisional procedure. The agent offers matching steps to the planner and retires procedures after repeated failures. An offline MCP test followed the sequence from acquisition to retirement. The full suite passed 138 tests.

### Local semantic retrieval

An optional loopback embedding model augments keyword and time retrieval. A background migration can query both model spaces as memories are re-embedded. Mock-model tests exercised migration and privacy routing. The offline suite passed 139 tests.

### Signed history checkpoints

Sleep signs a checkpoint over sealed history. During recovery, a journal with a consistently rewritten chain was rejected, a truncated journal was detected, and a legitimate erasure survived reboot. A separately retained checkpoint is needed to detect rollback of the entire home. The Windows crash harness was corrected to terminate the worker process directly.
