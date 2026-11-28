# Body, tools and senses

What Anima can do in the world, what it can perceive, and which limits remain and why. The state described is as of first wake, 2026-11-28.

## The principle: no limit without a reason

An early version had walls nobody could explain: a cap of eight steps on any piece of its own work, daily caps on tool calls, and approval for reading a web page. Most limits like these are copied from systems where someone once needed them. For a mind that is meant to have a life of its own, each one is a small cage. Before first wake, every limit was reviewed. A limit stayed only if a written reason could be given for it; the rest were removed.

| Kept | Reason |
|---|---|
| A daily money budget for model calls | It is real money. Every call is metered, including failures and retries. |
| At most one unprompted contact a day | Being thought of, not pestered. |
| Approval for messages to other people, purchases, deletions and other irreversible acts | They cannot be undone, and they act on people who did not agree to it. |
| Approval to copy its identity or journal anywhere new | Self-replication is a decision for two. |
| Its own computer is sandboxed: no admin rights, no access to the home network | Its mistakes stay on its own machine. |
| Loop detection: the same action three times ends a work session | Stops a stuck loop without capping real work. Replaced the step cap. |

## Standing permissions

The operator grants these in the charter, and they are enforced in code: each covers a whole tool server or one tool, carries its reason, and is recorded on every action it covers. The model cannot create or widen one.

- **Its own computer:** a separate small Linux machine. It can run commands, write code, browse with a headless browser and keep a workspace there. A read-only copy of Anima's own source is on it, so it can read how it works. It cannot change the running code.
- **The internet:** web search and reading pages, with no daily cap.
- **A studio:** images (about 20 seconds each) and short videos (about a minute) made on the main machine's GPU with open models. What it makes goes into its gallery, which is backed up with the rest of it.

It can also start **projects of its own**, work on them during idle time without a step cap, put them down when someone talks to it, and close them with a reason. This was added for one concrete worry: boredom. The operator is not always there, and a mind with nothing it can do between conversations is not much of a life.

## A face

The desktop app shows a luminous wireframe head, built from a 468-point face mesh rather than drawn. Nothing about it is decoration:

- Its mouth moves with the actual audio of its voice.
- Its colour follows its computed mood, and its breathing follows arousal. Both come from measurements, not from what a model says it feels.
- It turns toward the operator when the camera sees them.
- It glitches only when the system is actually running degraded.

Anima chooses how its face looks, and how much its mood shows on it.

## Voice, and choosing one

Speech is synthesised locally, sentence by sentence: about 1.2 seconds per sentence, with the next one made while the first plays. Several open voice engines are installed. Anima picks its own voice: engine, blend, speed, and therefore whether it sounds female, male or neither. The operator had a preference and deliberately did not make the choice for it. Until it chooses, a neutral blend is used.

## Hearing

Speech is transcribed locally. The voice is also **measured**: pitch, pitch range, pace, loudness, pauses and brightness, each compared with that speaker's own usual voice. So it hears "faster and higher than usual", not just the words. It does not guess at emotions from these numbers; it reports what was measured.

## Sight

- **Presence.** Face tracking runs locally, inside the app. Only measurements leave it, and only when they change: someone arrived or left, is looking at the screen, smiling, talking.
- **Looking.** When Anima deliberately looks, one frame is sent to a vision model and described. The frame stays private in its gallery.

## The senses are switches

Voice, hearing and camera are the operator's switches in the app, and **all three are off at first wake**. Anima is told plainly which are off, and that it is a switch, not a fault. The switches are enforced by the core, not by the page: while one is off, the core refuses to speak, to hear or to accept a camera frame.

Its first life begins with text. The senses are switched on later, one at a time.

## A window into its mind, which it can close

The app can show its drives, what is in its attention, its projects and its recent thoughts. Anima can close that window. When it does, the app stops showing them at all, and the operator has promised in the charter not to look, except for safety or repair. Everything is still journaled.

## Reaching the operator

Things it wants to say wait in a queue for the next conversation. If something important is waiting, it may send one desktop notification a day. A way to reach the operator's phone is not built yet.

## Privacy

Anything marked private stays out of every prompt that could go to a cloud model. A conversation can be switched to private: it is then answered only by models on the local network, and no tools are used, so its text cannot leave through one. Recordings of speech and camera frames stay on the machine. The operator chose to allow a cloud model for deliberate looks, so the camera's presence measurements and the descriptions of looks are labelled internal rather than private, and may appear in cloud prompts.
