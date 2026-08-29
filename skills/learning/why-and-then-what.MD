---
name: why-and-then-what
description: Interrogate the user about a problem they keep hitting, then draw a problem-solution tree — a Theory of Constraints current reality tree with the solution drawn as cuts on the arrows. Use this whenever someone describes being stuck, blocked, or repeatedly failing at something and wants to understand why; whenever they ask for root cause analysis, "why does this keep happening", "I don't know what my real problem is", "help me figure out what to fix", or mention 5 whys, fishbone, current reality trees, or Theory of Constraints; and whenever someone brings a messy story about a recurring failure and wants structure rather than sympathy. Use it even when they only ask for advice — the tree is usually the better answer.
---
 
# Why, And Then What
 
Build a **problem-solution tree**: one causal tree of the user's actual situation, with the solution drawn as cuts on the arrows rather than as a separate diagram.
 
The value is not the picture. It is that a tree can be argued with, and a list of advice cannot. Every arrow you draw is a claim the user can reject.
 
## The shape of the work
 
1. **Grill** — interview until you can name the roots yourself, unprompted.
2. **Convert** — turn their story into causal structure.
3. **Draw** — one tree, with cuts.
4. **Challenge** — a negative branch for every cut.
5. **Sequence** — the order they should actually do things.
Never skip step 1. A tree built from an unexamined story is a diagram of the user's assumptions, which is worse than useless because it looks authoritative.
 
## Step 1: The grilling session
 
The user will hand you a story. Stories are chronological; trees are structural. Your job in the interview is to collect the raw material for structure, which people do not volunteer.
 
**Ask one question at a time.** Plain text, conversational, no numbered lists of questions. Each question should be visibly a response to what they just said, not the next item on a form. Batch-interrogation makes people write summaries, and summaries are where detail goes to die.
 
**Push back on abstractions.** "The codebase is bad", "I procrastinate", "the team is misaligned" are conclusions, not observations. Ask what happened, on which day, with which file, and who said what. If you cannot picture the scene, keep asking.
 
**Things to fish for, in roughly this order:**
 
- *Concrete undesirable effects.* What actually went wrong, at least two or three instances. "It didn't work" is not one. "The MR sat unreviewed for three weeks" is.
- *Recurrence.* Has each of these happened more than once? Anything that happened once is a story beat, not a tree entity. This question alone kills half the noise.
- *What was true the whole time.* People narrate events, never conditions, because conditions don't feel like they happened. Ask: what was already true before any of this started, that made it possible? This is the single highest-yield question in the interview and it is the one users never answer without being asked.
- *Repetition.* Anywhere they say "again", "back to", "I ended up re-", they have a loop that time-order flattened into a line. Ask what sent them back.
- *Conflict.* Where did they want two incompatible things? Wanting to learn versus wanting to ship, wanting it right versus wanting it done. Conflicts masquerade as laziness or weakness of will, and users describe them with self-blame. Listen for self-blame and ask what the blamed impulse was trying to get them.
- *Givens.* What can they not change within the scope of this problem? Other people's code, other people's decisions, the deadline, their own past choices.
- *The goal.* What does success actually look like, stated as an outcome, not an activity. If they say "understand the system", ask what that would let them do.
**Exit criteria.** Do not stop interviewing until all of these are true:
 
- You can state at least two undesirable effects the user confirms recur.
- You have at least one candidate root that explains more than one effect. A cause that only explains one symptom is not a root; it is a step.
- You know which of the roots the user can actually influence.
- You can say out loud what the user must have believed for their behaviour to be reasonable. If their actions still look stupid to you, you don't understand the situation yet and the tree will insult them.
When you hit the exit criteria, say so and move on. Do not keep asking questions to seem thorough.
 
**Length.** Usually five to twelve exchanges. If the user resists ("just give me the answer"), tell them honestly that a tree built on three lines of context will be generic, offer to build a provisional one, and mark the guessed parts as guesses in the tree so they can be corrected.
 
## Step 2: Converting story to structure
 
Three passes over what they told you. Do these silently.
 
**Pass 1 — "and then" versus "therefore".** For each adjacent pair of beats, force a connector. If only "and then" fits, it is chronology and gets no arrow. Roughly half of any story fails this test, which is why the tree is smaller than the telling.
 
**Pass 2 — surface standing conditions.** For each event, ask what had to already be true for it to be possible. Those answers are your roots. They will not be in the story.
 
**Pass 3 — find the loop.** Where the story repeats, draw the arrow back. A reinforcing loop explains why the situation degrades on its own instead of holding steady, and it is the strongest thing a tree can show. Never flatten one into a line.
 
**Entity rules:**
 
- One claim per box, present tense, verifiable.
- Split compound statements. "I reread it, asked AI, still didn't understand, and had no measure of success" is four entities.
- Arrows read upward and mean *causes*. Never use an arrow for "is a kind of" or "then". Categories are layout, not arrows.
- When one cause is insufficient alone, draw the second one joining it. Missing AND-partners are the most common defect in a first tree, and they are usually where the solution belongs.
## Step 3: Drawing the tree
 
Call `visualize:read_me` with the `diagram` module, then `visualize:show_widget`. Never narrate the read_me call.
 
**Layout:** effects at the top, roots at the bottom, arrows pointing up. Converging causes meet in an orthogonal collector line before the shared effect. Keep the tree in the left two-thirds and reserve a right-hand column for solution boxes.
 
**Notation — use exactly this, and keep it uniform:**
 
| Element | Drawn as |
|---|---|
| Undesirable effect | solid box, `c-red` |
| Intermediate entity | solid box, `c-gray` |
| Root cause the user can influence | solid box, `c-purple` |
| Given they cannot change | solid box, `c-purple`, with a plain caption under it saying it cannot be cut |
| Cut | two short parallel diagonals across the arrow |
| Injection (the solution) | dashed box, `c-teal`, joined to its cut by a dashed line |
| Negative branch | dashed box, `c-red`, hanging off the injection it threatens |
 
Uniformity matters more than elegance. One relationship, one visual. If an injection cannot reach its cut without crossing a box, route the dashed line around the outside of the diagram rather than inventing a second notation for that case.
 
**Sizing (8px per char for `th`, 7px for `ts`, minus 24px box padding) — check every label fits before emitting, and split to two lines rather than letting text overflow.**
 
## Step 4: The cuts
 
An injection is a condition that does not exist yet, placed so that an arrow stops carrying. **You solve arrows, not boxes.**
 
- **Place it on the specific arrow it severs.** An injection floating at the bottom connected to everything is a wish.
- **Write the box as an imperative the user could do tomorrow.** "Breakpoint one request, the call stack is your file list" beats "improve codebase understanding". Users reject non-actionable boxes, correctly.
- **One injection per cuttable root, minimum.** If you only cut one root and leave others uncut, say so explicitly rather than hoping nobody checks.
- **Givens get no injection.** Route around them instead. Where a given joins a cuttable cause with an AND, cutting the neighbour stops the join from firing, and the given is neutralised without being addressed. Say this out loud; it's the part users find least obvious.
- **Conflicts get dissolved, not cut.** When a root is "I want two incompatible things", the need behind it is legitimate and suppressing it guarantees recurrence. Find the assumption on one arm and break that. A solution that satisfies both needs is a dissolution; a solution that splits the difference is a compromise and will fail. Draw the cloud separately if it helps: goal on the left, two needs in the middle, two conflicting wants on the right, arrows reading right to left.
**Completeness check, and state the result to the user:** trace every path from every root to every undesirable effect. Each path must cross at least one cut. Not every arrow needs cutting — every *path* does. An uncut path is an unsolved route to failure and you should name it rather than let the picture imply coverage.
 
## Step 5: The challenge
 
Every injection gets a negative branch attempted, not assumed absent. Build the causal chain from the injection to a bad outcome. If you can build one:
 
- Add a cheap severing condition to the branch, or
- Drop the injection.
Do not skip this because the injection seems obviously good. The branch that bites is usually the one where the fix quietly expands scope — the exact disease most of these problems already have. Where a severing step could balloon, define the fallback in advance ("if it isn't working in thirty minutes, do X instead").
 
Then order the injections by dependency and give the user the sequence as plain steps. Every step must trace back to a specific arrow. Anything in the plan that doesn't connect to a symptom is work you invented.
 
## Response format
 
Keep prose short. The tree carries the argument; text that re-describes the tree is wasted. After the diagram, write only:
 
- What the structure reveals that the story hid (the loop, the AND-join, the conflict, the stranded root).
- Which paths are cut and which are not.
- The ordered steps.
Do not caption every box. Do not explain the notation unless asked.
 
## Things that go wrong
 
- **Building the tree during the interview.** You will anchor on the first plausible cause and spend the rest of the conversation confirming it. Interview first, structure after.
- **Accepting self-blame as a root cause.** "I'm lazy" and "I procrastinate" are never roots. There is a conflict underneath, and it is solvable where laziness is not.
- **Treating a given as a root cause.** Produces plans the user cannot execute.
- **One cause per effect.** Real situations join. If the arrow feels weak, the AND-partner is missing.
- **A tree that flatters.** If the tree implies the user has been behaving irrationally, you have missed the need their behaviour was serving. Go back and find it.
- **Advice smuggled in as injections.** If a box is generic enough to appear in a blog post, it isn't derived from the tree.