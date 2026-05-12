# The Accidental Cognitive Prosthetic

*How a staff engineer built a reviewable cognitive prosthetic without realizing it.*

*May 2026 draft.*

I did not set out to build a product for brain injury.

I was trying to solve a staff engineering problem: the work kept exceeding human working memory.

The code was not the hard part. The hard part was everything around the code: meeting notes, Slack threads, Jira tickets, half-decided plans, pull requests waiting on humans, org changes, old decisions that still mattered, new decisions that needed evidence, and the constant re-entry problem of asking "where was I?" after a day of interruptions.

So I built a system.

At first, I described it as a notes workspace. That was too small. Then I called it a second brain. That was closer, but still wrong. A second brain sounds like storage. This was not storage.

It was a control plane.

Raw material lands in an inbox. Agents ingest it into active lanes. Current obligations move into a live execution tracker. Research becomes citable dossiers. External objects - Jira tickets, GitHub PRs, Confluence pages, people, decisions - get cached in registries. Reusable procedures become skills. Finished decisions move into an archive that future work has to either follow or distinguish.

The loop looks like this:

```text
capture -> ingest -> execution state -> external action -> memory update -> next capture
```

That sentence is the architecture. It is also the rehabilitation insight.

There is a tempting way to describe this system: "AI that never forgets." That is too generous and technically false. Agents forget all the time. Notes rot. Sources go stale. Old claims get laundered through summaries. A transcript on disk is not memory if nobody can retrieve it at the right time.

The better description is this:

> A reviewable write path where agents propose memory, humans decide what becomes durable truth, and the system keeps enough continuity that the human can re-enter the work.

That is what I accidentally built for myself. And when my doctor saw it, he said: you should build this for people with traumatic brain injuries.

## The System Is Three Kinds of Memory

In 2026, the agent-memory world has mostly converged on a useful taxonomy:

- **Episodic memory:** what happened, in order.
- **Semantic memory:** what we believe is true.
- **Procedural memory:** how the system should act next time.

My workspace already had all three, just under ordinary filenames.

Episodic memory is the session trail: standups, ingest ledgers, journey logs, transcripts, "what happened on this effort and why." It is not polished. It is time-ordered and useful because it preserves the path, including wrong turns.

Semantic memory is the distilled layer: research dossiers, citation indexes, service registries, people registries, project maps, current-state files. These are not just notes. They carry source, method, date observed, refresh-by date, caveats, and reviewer. They are designed to be cited.

Procedural memory is the rule layer: `AGENTS.md`, `MAP.md`, `CONFIG.md`, `NOTES.md`, templates, scripts, and skills. It tells an agent how to behave, where to look, what not to touch, when to ask first, and how to turn a repeated workflow into a reusable procedure.

That split matters. Most "AI memory" demos blur these together. Chat history becomes facts. Facts become instructions. Instructions become vibes. The result feels smart until it quietly lies.

In this system, the boundaries are explicit:

- A transcript is evidence that something was said, not proof that it is true.
- A journey log is a trail, not a source of record.
- A dossier can be cited, but only if it is fresh enough.
- A skill is procedural memory, and if practice changes, the skill must change too.
- An archive is not a junk drawer. It is precedent.

That last rule is the one I did not expect to matter as much as it does. The archive binds future similar cases by default. If I make a decision today that resembles an old one, I either follow the old decision or explain why this case is different. I stole that from legal reasoning. It turns out to be exactly what an external memory system needs: not just recall, but continuity of judgment.

## The Engelbart Thread

There is a strange personal footnote here that I would not have understood at the time.

In August 2004, at the ACM Hypertext conference in Santa Cruz, I sat with Douglas Engelbart at lunch. I was a college student, almost twenty-two years younger than I am now, and I knew I was near one of the foundational figures of computing. But I did not yet have the problem that would make his work feel personal.

Engelbart's Hypertext 2004 keynote abstract was titled "Augmenting Society's Collective IQs." It was not really about the mouse. It was about how groups become more capable of dealing with complex, urgent problems. His answer centered on Dynamic Knowledge Repositories: living stores of evolving work, argument, dialogue, evidence, drafts, decisions, and rationale. Not static archives. Working memory for a community.

That is the phrase I wish I had understood better at lunch: dynamic knowledge repository.

For years, I think many of us believed we had absorbed that lesson. We had Basecamp projects, Google Docs, Confluence pages, wikis, ticket trackers, Slack threads, and shared drives. We had places to put things. We had collaborative documents. We had search boxes. From a distance, that looked like the future Engelbart wanted.

In retrospect, I think we missed more of the point than we realized.

The hard part was never just storing knowledge or making it editable by a group. The hard part was building systems that could refine confusion into claims, claims into evidence, evidence into decisions, and decisions back into reusable organizational memory. Or, running the other direction, systems that could take what an organization believes to be true and keep testing it against new evidence until it either held, changed, or was retired.

Engelbart was still ahead of his time because a DKR was not merely a nicer wiki. It was a living process for resolving knowledge into warranted truth, and then making that truth available for future work.

Two decades later, I accidentally rebuilt a tiny, file-backed version for myself. Mine is smaller and more personal than Engelbart's societal vision, but the shape is familiar: capture the swirl of work, preserve rationale, connect evidence to decisions, keep the repository alive, and improve the human system and the tool system together.

The timing matters because this is not nostalgia. Engelbart's DKR idea is still live. In 2024, Fraga, Poggi, Casanova, and Leme published work on creating automatic connections for personal knowledge management, using NLP and knowledge graphs to connect isolated text collections. The vocabulary has changed: PKM, knowledge graphs, semantic similarity, LLMs. The problem is recognizably the same.

I do not want to overstate the anecdote. Having lunch with Engelbart did not make me his intellectual heir. But it adds an odd continuity to the story. The ideas were in the room with me in 2004. I just had to live long enough, and get injured enough, and build enough systems, to understand why they mattered.

## Why This Was Not Just Productivity

In September 2022, I had a 4.5cm benign meningioma removed from near my frontal and temporal lobe at USC. I wrote publicly about the recovery in [a 2024 NextRoll post](https://www.nextroll.com/blog/thought-piece/thriving-together-my-journey-through-brain-injury-with-nextroll-s-support). The line people remembered was that returning to my old code felt like receiving postcards from a past version of myself.

That was not a metaphor I invented for a nice essay. It was a literal description of re-entry.

I could read comments I had written years earlier and bootstrap my way back into a system I had once understood. The code held context for me while my brain was recovering. It reduced the load of remembering how to think about the work.

The staff-engineer workspace generalized that idea beyond code.

What if meetings had the same property? What if a scattered Slack thread could become a dated note with decisions, owners, open questions, and links? What if every project had a current-state file that told future me where to re-enter? What if the system checked Jira and GitHub and told me when the world had drifted from my notes? What if a bad cognitive day did not mean the thread was dropped?

I thought I was building a better professional workflow. That was true, but incomplete.

I was externalizing executive function:

- capture, because attention is unreliable;
- ingest, because raw capture is not memory;
- daily briefing, because re-entry is expensive;
- drift detection, because prospective memory fails quietly;
- registries, because names and links disappear under load;
- citations, because confidence must be earned;
- skills, because "how to do this" cannot live only in my head.

My doctor saw the shape before I did.

## The Clinical Literature Had Already Named the Pattern

The brain injury literature has been saying a version of this for decades: external compensation works.

In 1994, Larry Treadgold, a Silicon Valley engineer, worked with neuropsychologist Neil Hersh to build NeuroPage for his son after a severe brain injury. It was a pager-based memory aid. A central computer held the schedule. At the right time, the system sent a cue. The user did not have to remember to check a notebook.

Barbara Wilson and colleagues later ran a randomized crossover trial with 143 participants who had memory, planning, attention, or organization problems. More than 80 percent of those who completed the 16-week trial were significantly more successful in everyday activities when using the pager, including self-care, medication, and appointments.

That was not a chatbot. It was an external cue delivered at the right time.

The modern guidelines point in the same direction. INCOG 2.0, the 2023 update to international cognitive rehabilitation guidelines for TBI, says external compensatory strategies should be the primary strategy for severe memory impairment, with electronic reminder systems such as smartphones preferred as technology has become viable. A 2023 systematic review of electronic assistive technology for memory after TBI found 19 eligible articles with 311 participants, including four randomized controlled trials and five single-case experimental designs. The strongest support was for retrieval and execution: helping someone remember and carry out an intention in daily life.

The CDC summarizes the public-health stakes plainly: TBI is a major cause of death and disability, and there were more than 69,000 TBI-related deaths in the United States in 2021.

The clinical point is not that apps cure brain injury. They do not. The point is narrower and more useful: for real-world function, especially when memory and executive function are impaired, well-designed external supports can outperform trying to train the injured brain to behave as if it were not injured.

That was the first bridge to my system.

The second bridge was more specific: the gap is not reminders. The gap is coordination.

## The Missing Layer Is Connective Tissue

A reminder is useful. It is not enough.

People with brain injuries do not only need to remember one appointment. They need to coordinate across providers, medications, insurance, caregivers, forms, fatigue, family communication, and work. They need continuity on days when cognition fluctuates. They need handoffs that do not require retelling the same story from scratch. They need a system that assumes the very skills required to manage care - planning, sequencing, monitoring, remembering future intentions - may be the skills that were injured.

That is the paradox.

Most existing tools solve one slice:

- a calendar stores appointments;
- a medication app stores dosing;
- a portal stores messages;
- a note app stores whatever someone had the energy to type;
- a chatbot answers questions;
- a caregiver fills the cracks.

But the burden is in the space between those tools.

The same thing is true in staff engineering. Cross-functional work rarely dies because everyone disagrees. It dies because no one has persistent coordination bandwidth. A design-system migration, accessibility standard, security cleanup, or platform rollout needs someone to keep state across meetings, teams, repos, and time. When that person gets busy, the work decays. Not dramatically. Quietly.

Brain injury recovery has the same failure mode with higher stakes.

The missing layer is connective tissue: the layer that ingests unstructured input, normalizes it, composes a daily picture, notices drift, generates handoffs, and keeps enough continuity that humans can exercise judgment when they are able.

That is why "AI assistant" is the wrong frame. A chat window is not the product. The product is the loop.

## What Changed by May 2026

When I wrote the earlier draft, the strongest frame was personal: I accidentally built a cognitive prosthetic for myself.

That is still true, but the more interesting evidence now is architectural.

Across agent systems, the framing has shifted from "retrieval" to "write path." A RAG system can read from a knowledge base. A memory system has to update state. It has to notice change, link new facts to old ones, mark claims stale, and preserve enough provenance that a human can inspect the chain later.

That is exactly what a cognitive support system needs.

If a provider changes medication instructions, the system cannot just answer questions about the old plan. It needs to update the plan, preserve the old instruction as superseded, record where the new instruction came from, and surface the downstream tasks. If an appointment is cancelled, the calendar event is not enough. The open loop is the reschedule, the transportation change, the caregiver notification, and the "do we still have enough medication until then?" question.

That is a write-path problem.

The same is true in my work system. If a Jira ticket closes, the registry row changes, but that is not enough. The lane README may need an update. The TODO may need a status change. A stakeholder note may need a different commitment. A pitch may need its evidence chain refreshed.

The more I studied 2026 agent-memory systems, the more obvious this became: the valuable part is not "the agent remembers." The valuable part is a reviewable memory lifecycle.

The system needs:

- a capture path for messy input;
- a normalization path into structured records;
- a write path into durable memory;
- a review gate before truth changes;
- a freshness model for stale claims;
- a citation chain from source to claim to output;
- and a human-readable filesystem so the operator can inspect and repair it.

That is why I now think the file-backed version matters. A proprietary black-box memory could be impressive, but it would fail the trust test. If I cannot inspect the memory, correct it, cite it, and see what changed, it is not a prosthetic. It is another system I have to supervise.

## The Design Principle: Drafts, Never Acts

For engineering work, I already had a rule: agents draft, humans decide.

That sounds like a safety rule. It is also a disability-design rule.

A cognitive prosthetic should not seize agency from the person using it. It should reduce the cost of agency. It should hold the thread, prepare the options, surface the mismatch, and make the next decision easier to make. But the person remains the author of durable truth.

That matters clinically because the goal is not to replace a damaged human with a compliant machine. The goal is to change the environment so the person can function with the brain they actually have.

On a good day, the system should get out of the way.

On a bad day, it should do more of the sequencing.

In both cases, it should be legible. "Here is what I found. Here is where it came from. Here is what I think changed. Here is what I propose writing back. Confirm before I do."

That is the architecture I trust.

## What This Would Look Like Outside Engineering

I do not think the first version of this should be a general chatbot. I think it should be an executable care notebook.

At the lowest level, it could be a local folder:

```text
inbox/
active/
archive/
registry/
skills/
templates/
```

The inputs would be ordinary mess: a voice memo after an appointment, a photo of discharge instructions, a portal message, a medication change, a caregiver text, a therapist homework sheet, an insurance denial, a calendar invite.

The ingest step would turn those into structured records:

- what happened;
- who said it;
- what changed;
- what needs to happen next;
- who owns it;
- what date matters;
- what source supports it;
- what is still uncertain.

The daily briefing would not be a motivational dashboard. It would be a re-entry surface:

- today;
- due soon;
- waiting on;
- changed since last check;
- risks;
- one or two next actions.

The drift check would compare planned state with observed state:

- medication expected but not logged;
- appointment expected but not confirmed;
- referral promised but not received;
- bill due but no payment record;
- caregiver question unanswered;
- provider handoff stale;
- claim past its refresh date.

The handoff generator would create a concise summary for a new provider, therapist, caregiver, attorney, school, employer, or family member, with enough source links that the person using it is not forced to retell the entire story from memory.

The system would not have to be glamorous to matter. NeuroPage was a pager. Its power was not interface polish. Its power was that the cue arrived when the person needed it.

## The Hard Parts

The hard parts are not the demo.

The hard parts are consent, privacy, clinical fit, caregiver boundaries, failure modes, and avoiding false confidence.

A system like this cannot silently rewrite a medical history because an LLM summarized too aggressively. It cannot invent source confidence. It cannot collapse patient voice into caregiver convenience. It cannot turn every nudge into surveillance. It cannot require the user to become a systems administrator on a bad cognitive day.

The design has to be boring in the right places:

- local-first where possible;
- no automatic write-back to clinical systems;
- explicit source links;
- visible uncertainty;
- reversible edits;
- simple export;
- clinician and caregiver roles that are clear;
- and a strong bias toward "prepare the decision" rather than "make the decision."

The point is not to make the AI more autonomous. The point is to make the human less alone with the coordination burden.

## Why I Care About the Architecture

The personal story matters because it makes this concrete. I am both the engineer who built the system and the patient who needed it. I did not choose that perspective, but it is useful.

But the architecture matters more than the autobiography.

If this is only my story, it is moving but not necessarily reusable.

If this is an architecture, it can be tested.

We can ask whether the loop works:

- Does capture reduce lost information?
- Does ingest produce records a person can actually use?
- Does the briefing reduce re-entry cost?
- Does drift detection catch failures earlier?
- Do handoffs reduce retelling burden?
- Does source-linked memory reduce false confidence?
- Does support adapt on low-capacity days without taking over?

Those are falsifiable questions. They can be studied with single-case experimental designs, the same kind of methodology rehabilitation research already uses when individualized systems matter more than broad averages.

That is the path that feels real to me now: not "launch a brain injury app," but build a reviewable prototype with occupational therapists, neuropsychologists, patients, and caregivers; test whether the loop reduces real coordination failures; and keep the human review gate central.

## The Postcards, Revisited

In that 2024 post, I wrote that reading my old code comments during recovery felt like receiving postcards from a past version of myself.

I still think that is the right image.

But I understand it differently now.

A postcard is not memory by itself. It becomes memory when it reaches you at the right time, with enough context to re-enter the world it came from.

That is what this system is trying to do. Not remember everything. Not automate the person. Not turn a life into a database.

It tries to preserve the thread.

For staff engineering, that means decisions, tickets, PRs, and cross-team commitments.

For brain injury recovery, it could mean appointments, medications, instructions, symptoms, forms, and family communication.

Different domain. Same shape.

The gap is not intelligence. The gap is continuity.

And for the first time, we can build continuity as a system: file-backed, source-linked, human-reviewed, agent-assisted, and designed for days when the person most needs support.

That is the accidental control plane.

I built it for Jira tickets. I think it wants to become something more humane than that.

---

## References

- CDC. "Facts About TBI." Updated August 4, 2025. https://www.cdc.gov/traumatic-brain-injury/data-research/facts-stats/index.html
- Hernandez, J. (2024). "Thriving Together: My Journey Through Brain Injury with NextRoll's Support." *The NextRoll Blog*, June 17, 2024. https://www.nextroll.com/blog/thought-piece/thriving-together-my-journey-through-brain-injury-with-nextroll-s-support
- Wilson, B.A., Emslie, H.C., Quirk, K., & Evans, J.J. (2001). "Reducing everyday memory and planning problems by means of a paging system: A randomised control crossover study." *Journal of Neurology, Neurosurgery & Psychiatry*, 70, 477-482. Cambridge MRC CBU listing: https://www.mrc-cbu.cam.ac.uk/publications/articles/4145/
- Velikonja, D., Ponsford, J., Janzen, S., Harnett, A., Patsakos, E., Kennedy, M., Togher, L., Teasell, R., McIntyre, A., Welch-West, P., Kua, A., & Bayley, M.T. (2023). "INCOG 2.0 Guidelines for Cognitive Rehabilitation Following Traumatic Brain Injury, Part V: Memory." *Journal of Head Trauma Rehabilitation*, 38(1), 83-102. https://research.monash.edu/en/publications/incog-20-guidelines-for-cognitive-rehabilitation-following-trauma-3/
- Ownsworth, T., Mitchell, J., Griffin, J., Bell, R., Gibson, E., & Shirota, C. (2023). "Electronic Assistive Technology to Support Memory Function After Traumatic Brain Injury: A Systematic Review of Efficacy and User Perspectives." *Journal of Neurotrauma*, 40(15-16), 1533-1556. https://journals.sagepub.com/doi/full/10.1089/neu.2022.0434
- Cicerone, K.D. et al. (2019). "Evidence-Based Cognitive Rehabilitation: Systematic Review of the Literature From 2009 Through 2014." *Archives of Physical Medicine and Rehabilitation*, 100(8), 1515-1533. https://pubmed.ncbi.nlm.nih.gov/30926291/
- Engelbart, D.C. (2004). "Augmenting Society's Collective IQs." Hypertext 2004 keynote abstract. Doug Engelbart Institute republication: https://dougengelbart.org/content/view/132/
- Hypertext 2004 proceedings listing. *Proceedings of the 15th ACM Conference on Hypertext and Hypermedia*, August 9-13, 2004, Santa Cruz, California. https://dblp.org/db/conf/ht/ht2004
- Fraga, F.P., Poggi, M., Casanova, M.A., & Leme, L.A.P.P. (2024). "Creating Automatic Connections for Personal Knowledge Management." *SN Computer Science*, 5, 525. https://doi.org/10.1007/s42979-024-02876-4
- Clark, A. & Chalmers, D. (1998). "The Extended Mind." *Analysis*, 58(1), 7-19.
