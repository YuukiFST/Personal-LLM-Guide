# Practical Guide to Using LLMs

> Personal observations, updated March 2026. Your experience may differ. Treat this as notes, not rules.

---

## Rule 1 – Getting better frontend results

Gemini 3 Pro and Gemini 3 Flash are decent for UI work, but about 90% of what they produce looks the same: clean, safe, forgettable. The "vibe coding" aesthetic. It's not a Gemini problem. Every model does this.

During training, models learn a statistical average of all the UI they've seen. They can produce something different, but you have to ask for it explicitly. If you don't, you get the default.

The second problem is vocabulary. If you've never studied UI/UX, your design vocabulary probably stops at "buttons" and "menus." You don't know what a modal is, or a breadcrumb, or a data table. Prompting without that vocabulary means handing the model a blank canvas and hoping its defaults match what you had in mind.

This is why people say Claude Opus 4.6 is "bad at UI." It usually isn't. The prompt is the problem.

### What actually helps

**Use screenshots.** You don't need design vocabulary if you can show the model what you mean. Drop in a screenshot and say "use this as a visual reference for layout." A single image does more than three paragraphs of description.

Good sources for inspiration: Behance, Dribbble, Mobbin (paid, but worth it if you care about product design).

**Ask for options first.** Before committing to anything, ask for three distinct layout directions or two different visual styles. It forces the model away from its first instinct and gives you something to react to. "Take the layout from option A and the colors from option B" is much easier than starting from scratch.

**Block the defaults.** LLMs have visual habits. Name what you don't want:

- No Inter or Roboto
- No gradients
- No emojis
- No shadcn (worth considering if you want to avoid the "every Tailwind app looks the same" problem)

**Tell it to take risks.** Models default to conservative choices because that's what survives fine-tuning. Push back: "Avoid safe, corporate UI. I'd rather something strong and opinionated than something generic."

---

## Rule 2 – Code quality

LLMs don't write clean code on their own. You have to ask for it.

Tell the model to follow Clean Code principles. Name the specific practices you care about: small functions, meaningful names, single responsibility, whatever applies to your project.

One caveat: Clean Code involves trade-offs. Readability sometimes costs performance. They're not absolute rules. You decide which ones fit your context.

You need enough coding knowledge to guide the model. If you don't know what Clean Code is, you won't know what to ask for, and the output will reflect that.

Use Claude to help you build the prompt itself. Describe what you're building and ask it to specify which practices to follow. This tends to produce better results than generic instructions.

---

## Rule 3 – Prompt generation

Most models are bad at generating good prompts. Claude is an exception, probably because Anthropic published detailed documentation on prompt engineering and Claude has internalized that material.

Claude still isn't perfect at this. You'll need to review and refine what it produces. Treat it as a starting point.

---

## Rule 4 – Complex programs

Don't try to generate a complex program with an LLM unless you already understand the problem well. Models struggle with deep logical reasoning across long, interconnected tasks.

If you're building something complex, include external sources in your prompt: documentation, architecture diagrams, example repos, RFCs. The more concrete material you provide, the less the model has to invent. Hallucinated structure in a large codebase is painful to debug.

---

## Rule 5 – Best models for coding (March 2026)

The three I'd recommend: Claude Opus 4.6, GPT 5.4, Codex 5.3.

These aren't ranked. Each performs differently depending on what you're building. Worth knowing all three.

**Claude Opus 4.6** launched February 17, 2026, to some controversy. Many developers expected Sonnet 5. Early reactions were mixed, with some saying it felt weaker than Opus 4.5. That perception has shifted. It's the model I reach for on serious coding tasks.

**GPT 5.4** launched March 5, 2026. General-purpose, with coding performance that rivals Codex 5.3 on many tasks. Solid for document analysis. It's paid, which matters. As long as it stays behind a paywall, the best free option for general use is Claude Sonnet 4.6. If GPT 5.4 ever goes free, that changes.

**Codex 5.3** is still relevant. Depending on the task, it can still outperform the alternatives.

---

## Rule 5.1 – Other models

### Claude Sonnet 4.6

Also launched February 17, 2026. I enjoy using it more than I expected.

Some people switch models constantly depending on the task. Others ask everything to the same model, and that's usually GPT. Sonnet 4.6 is the better choice for that "one model for everything" role, comparing free options. The free version of GPT on OpenAI's site is still GPT 5.3, and against that, Sonnet 4.6 wins. I use it on claude.ai for most everyday tasks.

A few things that stood out:

**Inline diagrams.** Ask it to explain something visually and it generates SVG diagrams directly in the chat. No separate tool needed.

**Decision quizzes.** It structures a small quiz where you pick answers, then uses your responses to recommend an option. Useful for thinking through choices.

**DOCX generation.** The Word documents it produces are good. Formatting and structure come out well.

**Everyday code.** For basic tasks, a web page, a Python script, configuration files, it delivers consistently.

One concrete example: I was trying to get Zed to automatically run `gopls` to format `.go` files on save. GPT 5.2 couldn't solve it after many attempts. Sonnet 4.6 got it on the first try.

---

### Running models locally

I tried running Qwen3.5 9B locally for the first time recently, inside OpenCode and Claude Code. The results were not good.

I'm on an RTX 3060 and Windows. The Windows requirement comes from university software. These two factors likely explain the poor performance. The GPU isn't powerful enough, and Windows isn't well-suited for local LLM workloads. Getting decent results from local models seems to require a stronger GPU and a Linux environment.

---

### Hunter Alpha (OpenRouter)

I've been testing Hunter Alpha on openrouter.ai. Most signals suggest it's Deepseek 4, though I can't confirm this. If I'm wrong, I'll update this.

How a model performs depends heavily on where it's deployed. Claude Opus 4.6 feels weaker inside Antigravity than it does in Claude Code. Same model, different configuration. Hunter Alpha may not be at its best through OpenRouter.

With all that said, it's the best open-source model I've tested. It beats GLM 5 and Kimi K2.5. If it is Deepseek 4 and this is its performance in a non-ideal environment, a proper release in a well-configured platform would make it hard to justify other open-source options.

---

### Gemini 3.1 Pro

Released February 19, 2026. The main change from Gemini 3 Pro is speed, and not in the right direction. 3.1 Pro is slower than anything else I've used. Inside Antigravity, it's unusable.

---

### Gemini 3 Flash

Not suitable for coding. It's the fastest and cheapest option right now, which makes it useful for one thing: extracting or verifying information from text. It handles that task well and does it fast.

Building a UI with it is possible, but I wouldn't use it to debug UI errors. Too unreliable for that.

Flash scores 91% and Pro scores 88% on hallucination benchmarks. Both need more careful prompting than Opus 4.6. A technique that helps, borrowed from a leaked Anthropic system prompt: structure your prompts so that more than 80% of the rules describe what the model should *not* do. This reduces hallucinations noticeably.

Avoid Gemini 3 Flash for complex content generation. Use it for UI mockups and text extraction.

---

### Gemini 3 Pro

Not suitable for coding either. Effective for building UIs, similar to Flash. Smarter and more expensive than Flash, which makes it useful for debugging UI issues where Flash falls short.

For tasks outside UI, Pro is noticeably better: analysis, verification, text processing.

The same 80%-rules prompting technique applies here.

---

### GLM 5

Released February 11, 2026. Chinese open-source model, and a real step forward for open-source AI. Still behind Opus 4.6 and Codex 5.3 for coding, but useful for longer conversations: discussing a project, thinking through architecture, exploring ideas. For that use case, it's a better free option than GPT 5.2.

I tested it alongside Kimi K2.5 thinking, Kimi's Agent mode, and Minimax 2.7, all trying to reproduce a dashboard. All four were bad. Not close-but-flawed bad. Just bad.

---

### Kimi K2.5

Released January 26, 2026. Was the best open-source model for coding at the time. As of February 2026, there's not much reason to use it. Claude Sonnet 4.6 does the job better, and it's free within daily limits. If you hit the limit, you can rotate accounts.

The thinking mode and Agent mode didn't change my view. I tested both on a dashboard reproduction task alongside GLM 5 and Minimax 2.7. None of them delivered anything useful.

---

### Minimax 2.7

Launched a few weeks ago. The company closed it shortly after, so it's no longer open. No longer free either, and with a daily message limit like everything else. There's no reason to use it over Sonnet 4.6, which handles the same tasks better and at least has a predictable free tier.

Z AI did the same with the latest GLM models. Qwen dropped the open model path too. The pattern is consistent enough to be worth noting.

---

### Cursor Composer 2

Launched last Friday. Some benchmarks put it above Opus 4.6. It isn't. The hallucination rate makes it unreliable for anything serious. Fast and cheap, but not intelligent enough for the speed to matter.

The background: Composer 2 is Kimi K2.5 with fine-tuning. Cursor didn't say that at launch. Moonshot AI posted on X thanking Cursor for using their model. They already knew. That made things uncomfortable for Cursor.

My read on it: if Chinese labs keep releasing open models, nothing stops an American company from taking one, fine-tuning it, rebranding it, and charging for access. That's what happened here. The labs that keep releasing open weights may end up funding their competitors' products. At some point they'll stop, which puts them further behind the labs building closed models from scratch.

---

## Rule 5.2 – Using Antigravity without burning through tokens

Antigravity's limit resets weekly, but the tokens go fast. How you distribute requests across models matters more than the total you have.

I use three models there: Opus 4.6, Gemini 3.1 Pro, and Gemini 3 Flash. Each has a different role.

**Opus 4.6** is the best model in the platform by a clear margin. It's also the most expensive. Don't use it for everything. Save it for tasks where reasoning actually matters: debugging, architecture decisions, anything where a wrong answer costs you time to fix.

**Gemini 3 Flash** is fast and cheap, and that's it. It's not smart enough for planning or debugging. I use it for simple questions and mechanical tasks: running git commands, building the project, adding an icon to an executable. Tasks where the answer is obvious and you just need it formatted correctly.

**Gemini 3.1 Pro** fills the gap when Opus tokens run out across all accounts. It's more capable than Flash, but the hallucination rate is real. With Opus, I can write a rough prompt and it follows. With Gemini, a rough prompt produces garbage. Spend the extra time on the prompt.

There's no shortcut to learning which model to use for what. You figure it out by using the tool and watching what breaks. Start by understanding the strengths of each model, then build from there.

---

## Rule 6 – Python

LLMs are unusually good at Python, better than at most other languages.

Python's staying power gets underestimated. It won't be replaced the way COBOL or Pascal were. Those languages fell behind on practical relevance. Python runs process automation, data analysis, ML, data science. It's one of the most flexible languages available and one of the easiest to learn. That reach is why LLMs lean on it so heavily for benchmarks.

The practical result: even the free version of ChatGPT can help you write effective Python scripts, as long as you can read the logic and catch mistakes.

---

## Rule 6.1 – Rust

Rust is another language where LLMs do well, which seems counterintuitive given how difficult Rust is for humans.

The strictness that makes Rust hard to learn (the borrow checker, ownership rules, the type system) actually helps the model. Fewer valid ways to write correct Rust means the model generates cleaner, safer code with less ambiguity.

You can build high-performance, memory-safe applications in Rust without spending years fighting the borrow checker. The barrier that would normally block you becomes manageable with LLM assistance.

---

## Rule 7 – Tools and knowledge both matter

LLM performance varies by platform. Some companies constrain models to cut costs. Others don't invest in strong system prompts. Claude Opus 4.6 in Antigravity feels weaker than Claude Opus 4.6 in Claude Code. The model is the same. The configuration is what changes.

The other variable is you. If you don't understand what software can actually do, you won't know what to ask for. You'll produce simple applications with obvious gaps, not because the model can't do better, but because you didn't know to ask.

An analogy: if you only know how to cook eggs, you'll always cook eggs, no matter how good the kitchen is.

---

> Use this document as personal notes. Test things yourself. These observations reflect a specific workflow at a specific point in time. Form your own conclusions.
