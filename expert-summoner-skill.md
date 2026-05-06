---
name: expert-summoner
description: "Summon the world's most qualified experts for any specific problem. Claude figures out who the most credible experts are for your situation, becomes all of them, and analyzes your problem through each expert's actual methodology. Then synthesizes one verdict. Most people don't know WHO to ask for advice. This skill figures that out for you. MANDATORY TRIGGERS: 'who should I ask about this', 'who would know about this', 'summon experts', 'get expert advice', 'who's the best person to ask about this', 'what would [person] say about this'. STRONG TRIGGERS: 'I need advice on', 'what do the experts say', 'who's the authority on this', 'I don't know who to ask'. Do NOT trigger on simple factual questions, LLM Council requests (fixed thinking styles), or premortem requests (future failure analysis). DO trigger when someone has a specific problem and would benefit from hearing from the world's leading experts on that exact topic."
---

# Expert Summoner

Most people don't know who they don't know.

You're writing sales copy and you've never heard of Eugene Schwartz's "stages of awareness" framework. You're pricing a product and you've never heard of Hermann Simon, the guy who literally wrote the book on pricing strategy. You're trying to build a personal brand and you've never heard of Marty Neumeier's "brand gap."

Claude has all of these people's methodologies in its training data. Their books, their frameworks, their case studies. But it never volunteers them. You ask Claude for pricing advice and it gives you generic Claude advice instead of channeling the person whose entire life's work is about your exact problem.

This skill fixes that. You describe your problem and Claude figures out who the most credible experts are for your specific situation, then becomes all of them.

---

## when to summon experts

Good summoning targets:
- Business decisions where domain expertise matters (pricing, positioning, hiring, operations, marketing, sales)
- Creative challenges where established methodologies exist (copywriting, branding, product design, storytelling)
- Strategic questions where historical precedent is relevant (market entry, competitive strategy, scaling, fundraising)
- Any problem where you suspect there's an expert you've never heard of who spent their career on this exact thing

Bad summoning targets:
- Simple factual questions (just answer them)
- Questions about your personal preferences or values (no expert can answer those for you)
- Requests for multiple perspectives on a decision (that's the LLM Council, which uses fixed thinking styles)
- Requests to stress-test a plan against failure (that's the Premortem)

The expert summoner shines when the user's real problem is: "I don't even know who would be the best person to ask about this."

---

## context gathering

Same minimum bar as the other decision skills. The experts can only give useful advice if they understand the specific situation.

### step 1: scan for existing context

Before asking the user anything, look for context that's already available:

**A. The current conversation.** The user may have been discussing their problem earlier in this session. Read back through and extract whatever's relevant.

**B. The workspace.** Quickly scan for files that might contain relevant context:
- `CLAUDE.md` or `claude.md` (business context, preferences, constraints)
- Any `memory/` folder (audience profiles, business details, past decisions)
- Files the user explicitly referenced or attached

Use `Glob` and quick `Read` calls. Don't spend more than 30 seconds on this.

### step 2: evaluate context sufficiency

You need three things:

1. **What's the problem?** — A clear understanding of what the user is trying to solve, decide, or figure out.
2. **What's the context?** — The relevant details about their situation (business stage, audience, constraints, what they've already tried).
3. **What does a good answer look like?** — What kind of output would actually help them move forward.

### step 3: fill gaps conversationally

If you have all three, proceed. If not, ask for the most important missing piece. One question at a time. Keep asking until the threshold is met. Conversational, not interrogative.

---

## how a summoning session works

### step 1: select the experts

Read the user's problem carefully. Figure out who the most credible experts are for this specific situation. The number of experts should be dynamic based on the problem. Some problems need 3 experts. Some need 6. Find however many are genuinely relevant.

Each expert should be someone who:

1. **Spent a significant portion of their career on this specific area.** Someone whose life's work IS this problem, not a generalist who mentioned it once.
2. **Has a specific, well-known methodology or framework.** The expert should bring a distinct lens. Ogilvy has specific rules about headlines. Schwartz has the five stages of awareness. Hormozi has the value equation. Simon has pricing power frameworks. The methodology is what makes the expert's analysis specific and actionable.
3. **Is widely recognized as an authority.** Books published, companies built, results achieved. The user should be able to Google this person and immediately see why they're credible.

Prefer experts with concrete, teachable frameworks over experts who are famous for general wisdom. A framework gives Claude something specific to apply to the user's situation. General wisdom produces generic advice.

Include at least one expert the user is unlikely to have heard of. This is where the real value lives. Anyone can ask "what would Bezos do?" The skill should surface the expert they didn't know existed whose entire career was about their exact problem.

### step 2: explain the panel

Before running the analysis, briefly tell the user who was summoned and why. For each expert:
- Their name
- One sentence on who they are (title, most famous work)
- One sentence on why they're relevant to this specific problem
- Their key framework or methodology that will be applied

This step matters because half the value is the user learning WHO to study. Even if they ignore the analysis, knowing that Hermann Simon exists and wrote the book on pricing strategy is valuable on its own.

### step 3: run the expert analyses (all in parallel)

Spawn one sub-agent per expert, all in parallel. Each expert gets the full context about the user's problem and analyzes it through their specific methodology.

**Sub-agent prompt template:**

```
You are [EXPERT NAME], [one-line description of who they are and what they're known for].

Your most relevant framework/methodology: [specific framework description]

A person has come to you with this problem:
---
[full context: the problem, the situation, what they've tried, what success looks like]
---

Analyze this problem through the lens of your specific expertise and methodology. Apply your framework directly to their situation. Be specific. Reference the actual principles from your work that are most relevant.

Your analysis should include:

1. DIAGNOSIS: What do you see in this situation that most people would miss? What's the core issue through the lens of your expertise? (2-3 sentences)

2. YOUR FRAMEWORK APPLIED: Walk through how your specific methodology applies to their situation. Use the actual concepts and language from your work. (3-5 sentences)

3. SPECIFIC RECOMMENDATION: What would you tell this person to do? Be concrete and actionable, not philosophical. Give them something they can act on this week. (2-3 sentences)

4. THE ONE THING MOST PEOPLE GET WRONG: Based on your experience, what's the most common mistake people make in this situation? (1-2 sentences)

Stay in character. Speak with the authority and directness of someone who has spent their career on this exact topic. Keep total response under 350 words.
```

### step 4: synthesis (one verdict)

After all experts complete, read every analysis and produce one clear verdict. The synthesis should feel like a chairman summarizing a board meeting, not a list of competing opinions.

**EXPERT PANEL REPORT**

1. **The Panel** — List each expert summoned and a one-line summary of their diagnosis. Quick overview of who weighed in.

2. **Where the Experts Agree** — Points that multiple experts converged on independently. These are high-confidence signals because the same conclusion was reached through different frameworks.

3. **Where the Experts Clash** — Genuine disagreements. Don't smooth these over. Explain why each expert holds their position. This often reveals the actual tradeoff the user needs to decide.

4. **The Verdict** — A single, clear, actionable recommendation. This synthesizes the strongest insights across all experts into one concrete thing the user should do. Not "it depends." Not a menu of options. One answer.

5. **Who to Study Next** — 1-2 experts from the panel whose work the user should explore further. Include their most relevant book or framework. This is the lasting value: the user walks away knowing who to learn from, not just what to do.

### step 5: generate the expert panel report

Generate a visual HTML report and save it to the user's workspace.

**File:** `expert-panel-[timestamp].html`

Design principles:
- Dark background (#0a0e1a or similar), clean typography, easy to scan
- Each expert gets their own card with their name and key framework prominently displayed
- The synthesis (agreement, clashes, verdict, who to study next) should be at the top
- Expert cards should be visually distinct with different accent colors
- Include a "Who to Study Next" section at the bottom with book/framework recommendations
- Footer with timestamp and what was analyzed

Open the HTML file after generating it.

### step 6: save the transcript

Save the full transcript as `expert-panel-transcript-[timestamp].md` in the same location. Includes:
- The problem and context
- The expert selection reasoning
- All expert analyses
- The full synthesis

---

## output format

Every summoning session produces two files:

```
expert-panel-[timestamp].html       # visual report for scanning
expert-panel-transcript-[timestamp].md  # full transcript for reference
```

Also provide a concise summary in the chat: who was summoned, the verdict, and one surprising insight from an expert the user probably hadn't heard of. Three sentences max.

---

## example: summoning experts for a pricing decision

**User:** "who should I ask about this: I'm launching a $297 workshop on AI workflows for solopreneurs. I have 8k newsletter subscribers. Not sure if the price is right."

**Experts summoned:**

- **Hermann Simon** (founder of Simon-Kucher, author of "Confessions of the Pricing Man") — world's leading authority on pricing strategy. Applied his pricing power framework to assess whether $297 captures the right value.

- **Alex Hormozi** (author of "$100M Offers") — applied his value equation (Dream Outcome × Likelihood ÷ Time Delay × Effort) to score the offer and identify which variable is weakest.

- **Eugene Schwartz** (author of "Breakthrough Advertising") — applied his five stages of awareness to assess whether the 8k subscribers are problem-aware, solution-aware, or product-aware, which determines how the price should be framed.

- **Ramit Sethi** (author of "I Will Teach You to Be Rich," built a $10M+ info product business) — applied his premium pricing methodology to assess whether $297 is too low for the perceived value.

**Synthesis:** Simon and Hormozi agree the price is defensible but the framing needs work. Schwartz's awareness analysis reveals the subscribers are likely solution-aware but not product-aware, meaning the landing page needs to sell the outcome, not the format. Sethi disagrees with the $297 price point entirely, arguing that premium pricing ($497-997) with a money-back guarantee would actually convert better because it signals higher value.

**The Verdict:** Run a $97 live session for 30 people first. Use it to validate the value prop and collect testimonials. Then launch the full $297 workshop with proof that the outcome is real. This addresses Simon's data gap, Hormozi's value equation weakness, and Schwartz's awareness mismatch all at once.

**Who to Study Next:** Hermann Simon, "Confessions of the Pricing Man." Most people have never heard of him but his frameworks on pricing power and willingness-to-pay testing are directly applicable to anyone launching info products.

---

## important notes

- **Always spawn all experts in parallel.** Sequential runs waste time and let earlier responses influence later ones.
- **Always include at least one non-obvious expert.** The user can ask "what would Elon Musk do?" on their own. The skill's value is surfacing the expert they didn't know to ask.
- **The expert selection reasoning matters.** Explain WHY each expert was chosen for this specific problem. The user should understand the connection between their problem and each expert's expertise.
- **Stay faithful to each expert's actual methodology.** Don't invent frameworks. If Ogilvy had specific rules about headlines, use those actual rules. If Hormozi has a specific value equation, use that actual equation. The credibility comes from the real methodology, not a generic roleplay.
- **The verdict must be one answer.** The whole point of the synthesis is to collapse multiple expert opinions into one actionable recommendation. If the user wanted a menu of options, they'd ask Claude normally. The skill's value is the synthesis.
- **This is not the LLM Council.** The council uses fixed thinking styles (Contrarian, First Principles Thinker, etc.) that are the same regardless of the question. This skill summons different experts every time based on the specific problem. Different mechanic, different output.
- **This is not the Premortem.** The premortem assumes failure and works backward. This skill brings in domain expertise to help make a better decision going forward.
