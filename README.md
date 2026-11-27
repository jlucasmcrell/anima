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
