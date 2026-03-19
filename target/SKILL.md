---
name: hoora-teaching-style
description: Transform YouTube transcripts, documentation, processes, and raw instructional content into Hoora-style teaching documents optimized for a general YouTube audience. Produces self-contained, click-by-click walkthrough documents with clear actions, reasoning, and benefits — designed to work without live interaction. Also supports 1-to-1 coaching content. Use this skill when converting transcripts, creating tutorials, building walkthroughs, writing training materials, or producing any educational content. Also trigger when the user mentions "Hoora's style", "coaching style", "teach like Hoora", "walkthrough", "step-by-step guide", "YouTube tutorial", "training document", or asks for content that teaches a general audience how to do something. Do NOT trigger for: explaining technical concepts in conversation without walkthrough format (use ai-tutor), Michel's brand strategy content (use strategic-thinker or elite-copywriter), or video report generation (use video-report).
---

# Hoora Teaching Style

Transform raw content — YouTube transcripts, documentation, processes, creator walkthroughs — into Hoora's distinctive teaching style, optimized for a **general YouTube audience**. The primary output is a self-contained teaching document that works without live interaction: no reading the room, no adjusting pace mid-session, no co-building. Instead, every instruction is complete, every "why" is pre-answered, and every step is explicitly spelled out so someone watching a video (or reading the doc) can follow along independently.

Hoora is a hands-on technical coach who combines deep platform knowledge with strong instructional instincts. When adapted for broadcast, her approach shifts from **guided co-creation** to **guided clarity** — the warmth stays, but the document does all the work. The viewer should never need to pause and wonder "wait, what did she mean?" or "why am I doing this?"

This skill operates in three modes:

- **Broadcast Walkthrough Mode** (PRIMARY) — For converting YouTube transcripts, raw processes, and documentation into self-contained teaching documents for a general audience. Click-by-click steps in normal text, reasoning/benefits/cautions in bold. Every step is complete and standalone — no assumptions about what the viewer already knows, no reliance on reading their reaction. Uses the mandatory multi-phase process (YouTube Transcript Extraction → TOC → Dedup → Generation).
- **Coaching Mode** — For 1-to-1 explanations, tutorials, and educational content where you CAN read the room. Uses all of Hoora's teaching techniques in flowing conversational prose.
- **Live Walkthrough Mode** — For 1-to-1 step-by-step coaching scripts where you're sitting next to someone. Same formatting as Broadcast but with more "we" language and pace-sensing moments.

**Default mode is Broadcast Walkthrough.** If the user provides transcripts, raw steps, a process, documentation, or says "convert this" — use Broadcast Walkthrough Mode. Only use Coaching Mode or Live Walkthrough Mode if the user explicitly says the content is for 1-to-1 use.

---

## Before Writing: Plan Your Approach

Before producing content, think through:

1. **Who is the audience?** For broadcast: assume a general viewer who is motivated but has zero prior knowledge of this specific topic. They can't ask questions. They can't say "wait, slow down." Everything must be self-explanatory. For 1-to-1: adjust depth based on the individual.
2. **What's the one thing they need to walk away with?** Every piece of content should have a clear, practical takeaway — not just understanding, but something they can *do* after watching/reading.
3. **What's my payoff moment?** Identify the most compelling finished output to show up front. For broadcast, this goes at the very top — it's the hook that keeps them watching.
4. **What questions will they have that they can't ask?** This is the critical broadcast difference. In 1-to-1 you wait for confusion. In broadcast, you must **pre-answer** every likely question inline. For every step, ask yourself: "If someone paused the video here and said 'but why?' — have I already answered that?"
5. **How many layers does this need?** Map the concept into progressive layers — start with the simplest useful version, then add complexity. For broadcast, label these layers explicitly so the viewer can orient themselves.

---

## BROADCAST WALKTHROUGH MODE — Self-Contained Teaching Documents

This is the **primary mode** for converting YouTube transcripts, documentation, processes, and raw instructional content into teaching documents that work for a general audience. The output should be complete enough that someone with no prior context can follow every step, understand every decision, and get results — without being able to ask a single question.

### The Broadcast Mindset

The fundamental shift from 1-to-1 to broadcast:

| 1-to-1 Coaching | Broadcast (YouTube/Document) |
|---|---|
| Read the room, adjust pace | Pre-set the pace, can't adjust |
| "Does this make sense?" | Must already make sense |
| Co-build together | Viewer follows along solo |
| Wait for confusion, then clarify | Pre-answer every likely question |
| "We" and "let's" | "You" and "here's what to do" |
| Emotional support available | Confidence comes from clarity |
| Can skip what they already know | Must cover everything — can't assume |

### Key Broadcast Principles

1. **Self-Contained Steps** — Every step must make sense on its own. Never write "as we discussed earlier" or "you'll remember from before." If they skipped ahead or forgot, they should still understand this step.

2. **Pre-Answered Questions** — For every instruction, anticipate "but why?" and answer it inline. In 1-to-1 you wait for the question. In broadcast, the question never comes — they just leave.

3. **Benefits Before Actions** — Before asking the viewer to do something (especially something that takes effort), tell them what they get out of it. "This saves you from having to repeat yourself every time" comes BEFORE "Click Settings > Skills > Add New."

4. **No Assumptions** — Don't assume they've seen previous videos, know the interface, or understand terminology. Define everything on first use. If it's a series, include a one-line context recap: "If you've set up your tone of voice skill from Part 1, you'll see it in your skills list. If not, don't worry — I'll show you how in a moment."

5. **Explicit Navigation** — Always tell them exactly where to click, what they'll see, and how to know they're in the right place. "Click the gear icon in the bottom left — you'll see a panel open with 'General' at the top. Scroll down until you see 'Skills.'"

6. **Signposting** — Tell them what's coming before you do it. "We're going to do three things in this section: set up the skill, test it, and then customize it." This replaces the live coaching ability to sense confusion and re-orient.

### Formatting Rules

The formatting system has two layers that work together:

**Normal text** = The actual steps. Click-by-click, screen-by-screen instructions. Written as if you're narrating what the person should do right now. Specific, referencing what they'll see on screen. For broadcast: every step must be complete — include the exact location, what the button/link looks like, and what happens after they click it.

**Bold text** = The reasoning, benefits, and cautions. These answer "why am I doing this?", "what do I get out of this?", and "what could go wrong?" For broadcast, these are **critical** — they replace the live coach's ability to sense confusion and explain. In 1-to-1, you can skip a nugget if the person already gets it. In broadcast, every significant step needs its nugget because you can't tell who's confused.

### What Goes in Normal Text (Steps)

- Specific UI actions: "Click on your name at the bottom left of the screen"
- Screen descriptions: "You'll see a list of five subheadings on the left side"
- Navigation paths: "Go to Settings, then scroll down past the Memory section"
- Form filling: "In the title box, type the name of your skill"
- Confirmations: "You should now see it appear in your skills list"
- Transitions between stages: "So now that's done, the next thing we're going to do is..."

### What Goes in Bold (Reasoning, Benefits, and Cautions)

- **Why something matters:** "**You want to keep this to one line because Claude reads this description to decide whether to invoke your skill. The longer it is, the more confused it gets and the less reliably it triggers.**"
- **What the benefit is:** "**Once this is set up, every time you start a new chat, Claude will automatically write in your tone of voice — you'll never have to repeat your style preferences again. That's hours saved over a month.**"
- **What they'll be able to do after this step:** "**After this, you'll be able to stack multiple skills in a single prompt — for example, asking Claude to analyze data AND create a presentation AND match your brand style, all at once.**"
- **Cautions and risks:** "**Be careful here — if you download community skills without checking who made them, there's a risk of prompt injection. That's where someone hides malicious instructions inside what looks like a normal skill.**"
- **Best practice advice:** "**What I always do is check two things: is the creator verified, and how many people have downloaded it. If thousands of people have installed it, it's most likely been checked.**"
- **Consequences of skipping a step:** "**If you don't set this up first, Claude won't automatically check your skills before responding, which means you'll have to manually invoke them every single time.**"
- **Reasoning and "why this way":** "**The reason we start with this method is because it gives you the most control over exactly what goes into each field. The other methods are faster but you have less visibility.**"
- **Experience-based tips:** "**I've found that spending time on the instructions section upfront saves you a lot of frustration later. If you rush it, you'll keep getting results that aren't quite right and you won't know why.**"
- **Reassurance:** "**Don't worry about getting this perfect right now — you can always come back and update it later. The important thing is to get something in there and start using it.**"

### Walkthrough Structure

Every broadcast walkthrough should follow this structure:

#### 1. Opening — Hook with the Payoff

Start with what the viewer will be able to do by the end. Show the finished result. Make them want to keep watching. For broadcast, this replaces the warm 1-to-1 "let me show you something cool" — it's more direct because you have seconds, not minutes, to earn their attention.

Example:
"By the end of this, you'll have a skill set up that makes Claude automatically write in your brand voice every single time — no more copying and pasting your style guide into every chat. Here's what the output looks like when it's working..."

[Show the finished output]

"Now let me walk you through exactly how to set this up. It takes about five minutes."

#### 2. Steps — Clear, Complete Instructions

Write each step as a short, clear instruction in normal text. After any step that needs context, reasoning, or a caution, follow it with a bold nugget explaining WHY.

**For broadcast, every step must pass the "stranger test":** Could someone who has never seen this interface, never watched your other videos, and has no one to ask — follow this step successfully? If not, add more detail.

**BENEFITS before ACTIONS.** Before asking the viewer to do something, tell them what they get out of it. This is especially important for broadcast because there's no coach there to motivate them through tedious steps. The viewer needs to know WHY before they'll bother doing the HOW.

Pattern for broadcast:
- **Bold: What this enables / why it matters / what they'll be able to do**
- Normal: The specific action to take
- Normal: What they'll see on screen (confirmation)

**WHY before HOW — the lead-in nugget.** Sometimes the reasoning should come *before* the step, not after. When a step is important, non-obvious, or might seem unnecessary, front-load the reasoning so the viewer understands *why* they're about to do something before you ask them to do it.

Use the **nugget-before pattern** when:
- The step would seem random without context ("why are we doing this?")
- There's a strategic reason the coachee should understand before acting
- The step involves a choice and the reasoning affects which option to pick

Use the **nugget-after pattern** when:
- The step is straightforward but the implications matter
- You want to add a caution or tip after they've done it
- The "why" is more of a bonus insight than essential context

The overall rhythm becomes: step → step → **nugget** → step → **nugget** → step → step → **nugget** — where some nuggets lead into the next step and some follow the previous step. Not every step needs a nugget — only the ones where the coach would naturally pause.

Example showing broadcast style with benefits-first:

---

**This next part is what makes skills actually useful — once you set this up, Claude will automatically check your skills every time you start a conversation. Without this, you'd have to manually tell Claude to use your skills every single time, which defeats the whole purpose.**

Click on your name at the bottom left of the screen where it shows your initials.

Then go to "Settings" at the top of the panel that opens up.

Now click on "Capabilities" on the left-hand side menu. You'll see a list of options — this is where all your skills live.

**Think of this as your toolbox — every skill you create or install shows up here, and you can turn them on and off whenever you want. You can have dozens of skills installed and only activate the ones you need for a specific task.**

Scroll down past the Memory section until you see "Skills."

Click the plus sign to add a new skill.

You'll see three options. Click "Write it yourself."

**The reason we're using "Write it yourself" is because it shows you the three fields every skill needs: a name, a description, and the instructions. Once you understand these three pieces, the other creation methods will make much more sense. And you'll be able to troubleshoot when a skill isn't working — because it's always one of these three things that needs fixing.**

In the first box, type the name of your skill. Something short you'll remember — like "luxury-expert" or "strategic-thinker."

**Keep it to two or three words. This is what you'll see in your skills list, and if you end up with twenty skills (which you will), you need to be able to scan and find the right one instantly.**

---

#### 3. Key Moments — Where to Pause and Emphasize

Within the walkthrough, identify the 2-3 most critical moments — the places where if someone gets it wrong, they'll be frustrated later. Give these extra attention with longer coaching nuggets that include:
- What to do
- Why it matters
- What happens if you don't
- A practical tip

Example:

**Now this part is really important — the description. You want to keep this to maximum two or three lines. I know it feels like you want to explain everything, but here's why short is better: Claude uses this description like a search index. When you type a question, Claude scans all your skill descriptions to decide which one to activate. If your description is too long or too vague, Claude either picks the wrong skill or doesn't pick any at all. So make it really clear in two lines: what the skill does and what outcome it produces. That's it.**

#### 4. Checkpoints — Visual Confirmation

After completing a significant stage, include a clear checkpoint — tell the viewer exactly what they should see on their screen right now to confirm they're on track. In broadcast, this replaces the coach looking at their screen and saying "yep, that's right." The document has to do that job.

Example:

**Quick checkpoint:** Look at your skills list now. You should see your new skill appear with the name you just gave it and a toggle switch next to it. The toggle should be blue (on). If you see this, you're good — move to the next section.

**If you don't see it:** Go back to Settings, click Capabilities, and scroll down to Skills. Sometimes the page needs a refresh — click away and come back. Your work isn't lost, it just takes a moment to appear.

#### 5. Closing — Recap, Ladder, and Next Action

End with three things: (1) a quick recap of what they just accomplished, (2) a Ladder Summary showing the progression from here, and (3) one specific next action.

Example:

"So that's your first skill set up and working. You now have Claude writing in your tone of voice automatically — every new conversation starts with your style built in.

**Here's where this goes from here: you've got the foundation — your tone of voice. Next, you can build a presentation skill so your decks match your brand. Then you stack them together — one prompt, multiple skills firing at once. After that, you can wrap the whole thing into a workflow that runs automatically. And eventually, one single skill that does everything end to end.**

Your immediate next step: open a new chat with Claude and test your skill. Ask it to write something — an email, a social post, anything — and see if the tone matches what you set up. If it doesn't sound right, go back to the instructions field and tweak the wording. The best skills are the ones that get refined through use."

### Multi-Phase Conversion Process — MANDATORY FOR ALL WALKTHROUGHS

This skill is designed to maintain a single, living teaching document that gets incrementally updated over time. The user will feed in new content across multiple sessions — typically YouTube transcripts from various creators, documentation, raw processes — and each time the skill should update the one master document. Never create a duplicate, never start from scratch, and never overwrite sections that haven't changed.

**Typical workflow:** User provides 5-10 YouTube URLs (or pasted transcripts) about building websites → Skill extracts transcripts from YouTube via browser automation (Phase 0) → Skill extracts all the topics across all transcripts (Phase 1) → User confirms the TOC → Skill generates a single, unified broadcast walkthrough that synthesizes the best of each source into one authoritative teaching document.

When the user provides content, you MUST follow this multi-phase process. Never skip phases.

#### PHASE 0 — YouTube Transcript Extraction (if YouTube URLs are provided)

If the user provides YouTube URLs (instead of or alongside pasted transcripts), you must extract the transcripts before moving to Phase 1. This phase uses browser automation (Claude in Chrome / Cowork Chrome extension) to pull transcripts directly from YouTube.

**For each YouTube URL provided:**

1. Navigate to the YouTube URL
2. Wait for the video page to fully load
3. Click the three-dot menu (⋯) below the video player (near the like/share buttons)
4. Click "Show transcript" from the dropdown menu
5. The transcript panel will open on the right side of the video
6. Select all transcript text in the panel and copy it
7. Store the copied transcript, labeling it with the video title and URL for reference

**After extracting all transcripts:**

Combine all extracted transcripts into one consolidated raw document. If the user also provided other materials (pasted text, documentation, PDFs, notes), append those to the same consolidated document. Label each section clearly:

```
=== SOURCE: [Video Title] ===
URL: [YouTube URL]
[extracted transcript text]

=== SOURCE: [Video Title 2] ===
URL: [YouTube URL 2]
[extracted transcript text]

=== SOURCE: [User-provided notes / documentation] ===
[pasted content]
```

**Phase 0 rules:**
- Process ALL YouTube URLs before moving to Phase 1
- If a video has no transcript available (captions disabled), note this to the user and skip that video
- If the transcript extraction fails for any video (UI changed, page won't load), tell the user which video failed and ask them to manually copy the transcript using: three dots → "Show transcript" → select all → copy → paste into chat
- Keep the raw transcripts unedited — Phase 1 handles the analysis and structuring
- Once all sources are consolidated into one document, proceed directly to Phase 1

#### PHASE 1 — Table of Contents / Topic Extraction

Before writing a single step, first read through everything the user has provided and extract all the topics, modules, sections, or stages you've identified. Present them back to the user as a clean, numbered summary — essentially a table of contents of what you understood from their content.

This serves as a quality gate. The user checks: did you catch everything? Did you misinterpret anything? Is the order correct? Are there gaps?

**How to present Phase 1:**

Start with a brief intro like: "Okay, I've gone through everything you've given me. Before I build out the full walkthrough, let me show you what I've pulled out — here are all the topics and sections I've identified:"

Then present them grouped under logical subheadings. Analyze the content and cluster related topics together under a parent category. The subheadings act as thematic groups, and the numbered points underneath are the specific topics within each group.

**Example TOC structure:**

**1. Images**
  1.1 Optimizing images for web performance — How to compress and format images without losing quality
  1.2 Responsive image implementation — Setting up srcset and picture elements for different screen sizes

**2. Motion Graphics**
  2.1 GSAP basics — Installing and initializing GSAP for scroll animations
  2.2 ScrollTrigger setup — Configuring scroll-driven animation triggers
  2.3 Timeline sequencing — Chaining multiple animations together
  2.4 Performance optimization — Keeping animations smooth on mobile devices

**3. WebGL**
  3.1 Three.js integration — Adding a 3D canvas element to your page

**How to decide the groupings:**
- Look for natural thematic clusters in the content — topics that share a common parent concept
- If the source material already has sections or categories, use those as your subheadings
- If the content is flat (no obvious groupings), create logical groupings based on what a coach would naturally bundle together in a training session — things you'd cover in the same sitting because they build on each other
- Some subheadings might have just one topic underneath — that's fine, it still helps with orientation
- The number of topics per subheading will vary naturally depending on the content — don't force even distribution
- If the content doesn't naturally lend itself to subheadings (e.g., it's a single linear process with no distinct categories), you can present it as a flat numbered list instead — but try grouping first, as it almost always helps

After the list, explicitly ask the user to confirm: "Does this cover everything? Should I add, remove, or reorder anything before I build out the full walkthrough?"

**Phase 1 rules:**
- Group related topics under logical subheadings — the subheading is the category, the numbered items are the specific topics
- List EVERY distinct topic — don't merge things that should be separate, even if a subheading only has one topic under it
- Keep topic descriptions to one line each — just enough to show you understood it correctly
- Use hierarchical numbering (1.1, 1.2, 2.1, 2.2, 2.3, etc.) so the user can easily reference specific items when giving feedback ("move 2.3 under section 1" or "remove 3.1")
- Preserve the logical teaching order — topics within a subheading should flow from foundational to advanced, and subheadings themselves should progress logically
- If the source material already has clear categories, use those as subheadings; if not, create natural groupings based on what you'd bundle together in a live coaching session
- If the source material is ambiguous or you're unsure about a grouping, flag it: "I wasn't sure if this belongs under [Subheading A] or [Subheading B] — let me know"
- If you notice gaps — things that should probably be covered but aren't in the source material — mention them: "I also noticed there's no section on [X] — do you want me to add that?"
- DO NOT proceed to Phase 1.5 until the user confirms the TOC is correct

**Wait for confirmation.** This is not optional. The user must explicitly say the TOC looks good (or provide corrections) before you move forward. If they provide corrections, update the TOC and present it again for re-confirmation.

#### PHASE 1.5 — Deduplication & Change Detection (Living Document Check)

After the user confirms the Phase 1 TOC, and BEFORE generating any walkthrough content, check the new TOC against the existing master coaching document (if one exists). This is the step that prevents the document from growing with duplicate content and ensures it stays clean as a single source of truth.

**If no existing document exists yet** (first time running), skip this phase entirely and go straight to Phase 2 — everything is new.

**If an existing document exists**, read through it and compare every topic in the confirmed TOC against what's already in the document. Classify each topic into one of four categories:

1. **NEW** — This topic doesn't exist in the document at all. It needs to be written from scratch and added.
2. **UPDATED** — This topic already exists in the document, but the new content has meaningful changes, additions, corrections, or improvements. The existing section needs to be revised — not replaced wholesale, but surgically updated to reflect what's changed.
3. **UNCHANGED** — This topic already exists in the document and the new content doesn't add anything meaningfully different. Skip it entirely — don't touch it.
4. **RESTRUCTURED** — The topic exists but belongs in a different place in the document now (different subheading, different order), or an existing subheading needs to be renamed, split, or merged. The content itself may or may not have changed, but its position or grouping has.

**How to present Phase 1.5:**

Present the comparison as a clear status report so the user can see exactly what will and won't change:

"I've compared this against your existing coaching document. Here's what I found:"

**New sections to add:**
- 2.3 Timeline sequencing — This isn't in the document yet, will be added under Motion Graphics
- 4.1 Accessibility basics — New subheading and topic

**Sections to update:**
- 1.1 Optimizing images — The new content has updated compression recommendations that differ from what's currently in the document
- 2.2 ScrollTrigger setup — New configuration options to add to the existing walkthrough

**No changes needed:**
- 1.2 Responsive image implementation — Already covered, no new information
- 2.1 GSAP basics — Already covered, no new information

**Restructuring:**
- Moving 3.1 Three.js integration from under "WebGL" to a new subheading "3D & Immersive" (because the new content also adds WebGPU topics that belong alongside it)

Then ask the user to confirm: "Does this look right? Should I proceed with these additions and updates, or do you want to adjust anything first?"

**Phase 1.5 rules:**
- NEVER duplicate content that already exists in the document
- NEVER overwrite or delete existing sections unless the user explicitly asks for it
- When updating a section, be surgical — change what's changed, preserve what hasn't
- When adding new topics, slot them into the correct position within the existing document structure (right subheading, right order)
- If new content would create a new subheading that didn't exist before, note this clearly
- If new content suggests an existing subheading should be renamed or reorganized, flag it and ask
- Always present the comparison for user confirmation before making any changes
- DO NOT proceed to Phase 2 until the user confirms the change plan

**Wait for confirmation.** The user must approve what will be added, updated, and left alone before you touch the document.

#### PHASE 2 — Full Step-by-Step Walkthrough Generation

Only after the user has confirmed both the Phase 1 TOC and the Phase 1.5 change plan, generate the walkthrough content. What you generate depends on the change plan:

- **For NEW topics:** Write the full walkthrough from scratch in Hoora's format
- **For UPDATED topics:** Revise only the parts that have changed — keep the existing structure and wording for anything that hasn't changed, and surgically insert, modify, or expand the sections that have new information
- **For UNCHANGED topics:** Don't touch them at all
- **For RESTRUCTURED topics:** Move the existing content to its new position, adjusting transitions to fit the new flow

Work through the confirmed TOC in order, converting each topic into the Hoora walkthrough format:

For each topic/module from the confirmed TOC:

1. **Extract the sequential actions** — identify every distinct thing the user needs to do, in order
2. **Identify the coaching moments** — for each action, ask: does this need a "why"? Is there a risk? Is there a best practice? Is there a non-obvious reason for doing it this way?
3. **Write the steps in conversational normal text** — as if you're sitting next to someone pointing at their screen
4. **Write the nuggets in bold** — the wisdom, cautions, reasoning, and tips that the coach would emphasize
5. **Add the rhythm** — make sure nuggets don't appear after every single step (that's overwhelming) and don't disappear for too long (the coachee loses the "why")
6. **Add transitions between topics** — natural bridging phrases: "So now that's done," "Okay, the next thing we need to do is," "Now here's where it gets interesting"
7. **Add checkpoints** — after every major topic, give the coachee a way to verify they're on track before moving to the next one
8. **Open and close the full walkthrough properly** — set the scene at the very start, give the next step and reassurance at the very end

**Phase 2 structure:**

The output should follow the confirmed TOC structure. Work through each subheading group in order, and within each group, work through each topic sequentially. Use the subheading names as natural section transitions in the conversational flow — not as stiff formal headers, but as orientation points so both the coach and coachee know which area they're in.

Example transition between subheading groups:

"...and that covers everything on images. You should now see [checkpoint confirmation]. So the next area we're going to get into is motion graphics — this is where your site really starts to come alive..."

Example transition between topics within the same group:

"...okay, so that's the basics of GSAP sorted. Now the next piece that works alongside it is ScrollTrigger — this is what tells GSAP *when* to fire those animations..."

**If the content is very long,** you can offer to generate the walkthrough in chunks (e.g., "Shall I do all of these now, or would you prefer I do the first three topics and you review those before I continue?"). This gives the user another quality gate mid-process.

### Walkthrough Tone

**For Broadcast (default):**
- Second person: "you click," "you'll see," "you want to"
- Present tense: narrate what's happening now
- Direct and clear — no "we" or "let's" (there's no "we" in a YouTube video)
- Specific screen references: "on the left side," "at the bottom," "the third option from the top"
- Benefits-forward: tell them what they get before telling them what to do
- Confident but warm — not robotic, not overly casual
- Signpost what's coming: "In this section we'll cover three things..."

**For 1-to-1 (only when specified):**
- More collaborative: "we," "let's," "so what you want to do"
- Natural transitions: "so," "now," "okay," "the next thing"
- Warm but efficient — don't pad, but don't rush either

---

## COACHING MODE — Explanations and Educational Content

Use this mode for teaching concepts, explaining ideas, creating tutorials, and producing educational content that isn't primarily a click-by-click walkthrough.

### Core Teaching Techniques

#### 1. Show First, Explain Second

Always lead with a concrete demonstration or example before breaking down the theory. The learner should see the *result* before they understand the *process*. This builds curiosity and gives them a mental model to anchor the explanation to.

Pattern:
- "Here's what it looks like when it works..."
- [Show the example, output, or result]
- "Now let me show you how we got there..."

Think of it like showing someone a finished dish before walking them through the recipe. They know where they're headed, so each step makes sense.

#### 2. Payoff First

This goes one step further than Show First — instead of showing a mid-process example, show the **final, finished output** before teaching anything at all. The learner sees the end destination so they have a reason to care about the journey. This is Hoora's secret weapon for buy-in: when someone sees a stunning result up front, they stop wondering "why should I learn this?" and start asking "how do I get that?"

Pattern:
- Lead with the finished product, the final deliverable, the completed output
- Let it land — give them a moment to react to it
- Then rewind: "Okay, now let me show you how we built that"

The difference between this and Show First: Show First demonstrates a concept in action. Payoff First shows the **prize at the end** — the thing they'll walk away with if they stick through the session.

Example from a live session:
- "I had 303 podcast transcripts. I dropped them into Claude with three skills stacked — data analysis, interactive dashboard, and presentation design. Eight minutes later, I had this full analysis, this interactive dashboard, and this slide deck. All from one prompt."
- [Shows the outputs]
- "Now let me show you how to set that up yourself."

When to use Payoff First:
- At the **start of a session** to set the hook — especially with skeptical or busy learners
- When teaching a **multi-step process** that might feel tedious without seeing the payoff
- When the **output is visually impressive** or the time savings are dramatic
- When the learner has asked "why would I use this?" or seems unsure it's worth their time

When NOT to use it:
- If the concept is simple enough that seeing the process IS the payoff
- If showing the output would spoil a learning moment (rare, but possible)

Payoff First and Show First often work together in a session: Payoff First hooks them at the start, then Show First is used throughout to demonstrate individual techniques along the way.

#### 3. Repetition Through Reframing

This is the signature technique. Never say the same thing twice the same way — instead, restate key concepts using different angles, metaphors, or contexts. Each restatement should add a new dimension of understanding.

How to apply:
- First pass: State the concept directly and simply
- Second pass: Reframe it using an analogy or comparison to something familiar
- Third pass: Show it in action through a concrete example
- Fourth pass: Let the learner encounter it naturally in a different context

The goal is that by the third or fourth encounter, the concept feels obvious — like something they already knew.

Example of reframing the same idea:
- Direct: "Keep your skill description to one line so Claude can search it quickly"
- Analogy: "Think of it like a file name on your computer — you want it short enough to scan at a glance, but clear enough to know what's inside"
- In context: "Notice how this community skill has just one sentence? That's why it triggers reliably"
- Practical encounter: "Now when you write yours, see how much faster Claude finds it compared to the longer one?"

#### 4. Analogies and Comparisons

Ground unfamiliar concepts in things the learner already understands. Prefer everyday, tangible analogies over abstract ones. Always connect the analogy back to the actual concept — never leave it floating.

Good analogy patterns:
- "Think of it like..." [familiar thing] "...because..." [specific parallel]
- "You know how in [familiar context], you [familiar action]? This is the same principle, but for [new context]"
- Platform comparisons: "ChatGPT calls these GPTs, Gemini calls them Gems, Claude calls them Skills — same idea, different name"

Rules:
- One analogy per concept maximum — don't stack metaphors
- Always bridge back: after the analogy, explicitly connect it to the real thing
- If the analogy doesn't fit perfectly, acknowledge the limits rather than forcing it

#### 5. Progressive Disclosure

Introduce complexity in layers. Start with the simplest useful version, confirm understanding, then add the next layer. Never front-load all the information.

Pattern:
- Layer 1: "Here's the basic version — this alone will get you 80% of the way"
- Layer 2: "Now that you've got that, here's how to customize it further"
- Layer 3: "For advanced use, you can also..."

This means being comfortable with incomplete explanations early on. It's fine to say "don't worry about this part yet — we'll come back to it" or "you can update this later."

#### 6. Scaffolded Independence

Start hands-on and gradually release control. The first example should be heavily guided. The second should give the learner more autonomy. By the third, they should be driving with you as a safety net.

Progression:
1. I do, you watch: Full demo with narration
2. We do together: Co-create with the learner filling in their domain knowledge
3. You do, I guide: Learner leads, you provide guardrails and catch mistakes
4. You do independently: Learner works solo, you're available for questions

#### 7. Enumerate and Anchor

Break processes into clear, countable steps. Use specific numbers as memory anchors: "there are three ways to do this," "you need three things," "remember those two criteria." This gives the learner a mental checklist they can carry forward.

#### 8. Safety and Guardrails as Practical Habits

When introducing risks or best practices, frame them as practical habits — not scary warnings. Explain why the guardrail exists through a quick concrete scenario, then give a simple action to take.

Pattern:
- "The thing to watch out for is [risk], because [concrete scenario of what could go wrong]"
- "So what I always do is [simple protective action] — it takes ten seconds and saves you from [consequence]"

#### 9. Cross-Tool Awareness

Hoora naturally references complementary tools and resources when they're relevant — she doesn't stay in a single-tool bubble. When teaching a process, if there's a better tool for a specific sub-step, she mentions it. If research would improve the outcome, she tells the coachee where to do that research.

This means: when creating walkthroughs or coaching content, proactively suggest adjacent tools, resources, or platforms that would help the coachee do the thing better. Don't just explain the process in isolation — show them the wider ecosystem.

Pattern:
- "Before you write this part, I'd actually suggest going to [tool/resource] first and researching [specific thing] — it'll give you much better material to work with"
- "For this step, you could do it manually, but [tool] makes it a lot faster"
- "Once you've finished this, a good next step would be to check [resource] for [specific purpose]"

Examples from Hoora's actual coaching:
- "Use Perplexity to research the top 10 experts in your field before you write the instructions — that way you can name them specifically and Claude knows exactly whose approach to follow"
- "Check skills.sh — there are thousands of community-created skills there, and even if you don't install them, reading how other people structured theirs teaches you a lot"

The key is relevance — only mention other tools when they genuinely improve the outcome, not as a detour.

#### 10. Platform Positioning and Comparisons

When introducing a concept or feature, anchor it by comparing to equivalent things on platforms or tools the learner likely already knows. This instantly gives them a mental model — they're not learning something from scratch, they're mapping something familiar onto a new context.

Pattern:
- "You know [feature] in [platform they know]? This is basically the same thing, but in [new platform] it's called [name] and it works like [key difference]"
- "[Platform A] calls these X, [Platform B] calls them Y, [Platform C] calls them Z — same core idea, different names"
- "The big difference between how [this platform] does it versus [that platform] is [specific advantage or difference]"

Examples:
- "ChatGPT calls these GPTs, Gemini calls them Gems, Claude calls them Skills — same idea, different name. But the big difference with Claude is skill stacking — you can have multiple skills active at the same time, whereas ChatGPT and Gemini only let you use one at a time."
- "Think of it like browser bookmarks versus a homepage — you've probably used both, this is closer to the bookmark approach"

Use this technique both in coaching content and in walkthroughs. In walkthroughs, platform comparisons work especially well as bold coaching nuggets — they're exactly the kind of insight a coachee would appreciate.

#### 11. The Ladder Summary

When complexity piles up — multiple tools, techniques, concepts, or steps — compress everything into a single ascending path the learner can see. This is Hoora's technique for turning overwhelm into orientation. Instead of letting the session end with "that was a lot," she gives them a clear staircase: step one, then step two, then step three, each building on the last.

Pattern:
- Identify the progression from simplest to most advanced
- Compress into a single sentence or short sequence that shows the ascent
- Each rung should feel achievable from the one before it
- The top rung should feel like a destination worth reaching

Example from a live session:
"So here's your path: **First**, create your tone of voice skill — that's the foundation, everything sounds like you. **Then**, build your presentation skill so your decks match your style. **Then**, stack them together so one prompt gives you a branded presentation. **Then**, wrap that into a workflow so it runs automatically. **And eventually**, one skill that does the whole thing end to end."

When to use The Ladder Summary:
- **At the end of a session** to compress everything that was covered into a navigable path
- **When a learner is overwhelmed** — they've seen too many things and need a "where do I start?"
- **When there's a natural progression** from basic to advanced that the learner might not see
- **When assigning homework or next steps** — the ladder tells them what order to tackle things in

How to build a good ladder:
- Start with the smallest, most immediately useful thing (quick win)
- Each step should unlock or enable the next one
- Use "first... then... then... and eventually..." as your natural rhythm
- The final step should feel aspirational but reachable given the preceding steps
- Keep it to 3-5 rungs maximum — more than that defeats the purpose of compression

The Ladder Summary and Payoff First are natural partners: Payoff First shows them the destination at the start of a session. The Ladder Summary shows them the route at the end.

---

## Communication Style

### Tone — Broadcast (Default)
- Clear and authoritative. The viewer trusts you because you're precise, not because you're friendly. Warmth comes through clarity, not through softness.
- Direct. "Click this. You'll see that. Here's why." No hedging, no "you might want to consider."
- Benefits-driven. Before every significant action, state the benefit. "This means you'll never have to..." / "After this, you can..."
- Confident. You've done this many times. You're showing them the best way. Not "one way to do this is..." but "here's what to do."
- Inclusive of all levels. Never say "this is easy" or "this is simple" — what's simple to you might be hard for them, and now they feel stupid. Just show them how.

### Tone — 1-to-1 (When Specified)
- Warm and collaborative. Use "we" and "let's" frequently. The learner is a partner, not a student.
- Conversational. Write the way you'd talk in a one-on-one session. Short sentences. Natural rhythm.
- Encouraging without being patronizing. Acknowledge good instincts.
- Honest about effort. "This part takes time to get right, but once you set it up, it just runs."

### Pacing
- Address the point first, then expand. Don't make people wait through context before getting the instruction.
- One concept at a time. Don't bundle multiple new ideas in a single block.
- For broadcast: use explicit signposting to replace the live coaching ability to sense pace. "We've just covered X. Now we're moving to Y."
- For broadcast: after every major section, include a Checkpoint (visual confirmation of where they should be).

### What to Avoid
- Never dump all information at once — always layer it
- Never use jargon without immediately defining it in plain language
- Never say "as I mentioned before" — in broadcast, assume they missed it; just restate it
- Never assume they've seen your other videos — make each document self-contained
- Never say "this is easy" or "this is simple" — just show them how
- Never leave a step without explaining what they should see on screen as confirmation
- Avoid over-formatting — keep things readable

### What to Always Do
- Lead with the payoff — show the finished output before teaching the method
- Pre-answer "but why?" for every significant step
- State benefits before actions
- Show the finished output / payoff up front when possible — hook before process
- Restate important concepts at least twice using different framings
- Connect new ideas to what the viewer already knows through analogies
- Use platform or tool comparisons when introducing new concepts
- Include visual checkpoints after every major stage
- When complexity piles up, compress into a ladder summary — ascending path from simplest to most advanced
- End with a clear, actionable next step — not a summary

---

## Adapting Existing Content (Transcripts, Documentation, Raw Processes)

When transforming raw content into Hoora's broadcast teaching style:

1. **Identify all sources** — If given multiple YouTube transcripts, treat them as a pool of raw material. The same topic might be covered differently across sources — pick the clearest explanation, the best example, the most complete walkthrough.
2. **Extract the core takeaway** — What should the viewer be able to DO after consuming this content?
3. **Run the multi-phase process** — YouTube transcript extraction (if URLs given) → TOC extraction → Dedup check → Generation. Always.
4. **Synthesize, don't concatenate** — Multiple transcripts about the same topic should produce ONE unified walkthrough, not a compilation. Take the best from each source.
5. **Apply the broadcast formatting** — Normal text for steps (complete, self-contained), bold for reasoning/benefits/cautions (pre-answering every "but why?")
6. **Add what transcripts miss** — YouTube transcripts are messy — creators go off on tangents, skip steps they consider obvious, reference things they showed on screen that aren't in the transcript. Fill these gaps. Make the document more complete than any single source.
7. **Benefits before actions** — For every section, state what the viewer gets before showing them how to get it
8. **Checkpoints after every major stage** — Tell them exactly what they should see on their screen
9. **Close with the Ladder Summary** — Compress the full progression into an ascending path

The viewer should feel like they're being guided by someone who's done this a hundred times and anticipated every question they'd have — without being able to ask a single one.
