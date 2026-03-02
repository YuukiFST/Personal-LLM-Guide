# Practical Guide to Using LLMs - Personal Experiences

> **Important Notice**: This document reflects my personal experiences and opinions based on practical use of different LLMs over time. The observations described here may not apply to all use cases and may vary depending on context, tools used, and model evolution.

This guide contains observations that I have not found in other official documentation. I refer to the numbered items below as **"rules"** to facilitate cross-references.

**Last update of my experiences**: February 2026

---

## Rule 1 – UI Design, LLM Behavior, and How to Get Better Frontend Results

**In my experience**, the best LLMs for UI design are **Gemini 3 Pro** and **Gemini 3 Flash**.
However, I’ve noticed they tend to generate very similar UIs about 90% of the time. If you’re used to looking at LLM outputs, you quickly see that the design follows a very specific **“vibe coding”** style: clean, safe, and a bit too generic.

This behavior isn’t unique to the Gemini family, it’s more of a general pattern in how LLMs handle frontend.

### Why this happens

LLMs converge on a sort of **“default” UI style** during training, basically the average of everything they’ve seen. They absolutely *can* produce something different, but you need to **ask for that difference explicitly**.

It’s similar to how ChatGPT (or any other LLM) talks: by default, it responds in the same neutral tone to everyone until you say “be sarcastic” or “explain like I’m five”. Frontend generation works the same way. If you don’t specify a direction, the model falls back to its safe, predictable templates.

There’s another important issue: most of us aren’t very good at **describing design precisely**.

If you’ve never studied or worked with UI/UX, your entire vocabulary for interfaces probably stops at “buttons” and “menus”. You don’t know the names of other components (cards, modals, breadcrumbs, sidebars, accordions, tooltips, data tables, carousels, and so on). When you try to prompt an LLM for a UI without knowing these terms, you lose the ability to tell it what you actually want. You end up fully dependent on whatever default style the model decides to use.

This is one of the main reasons people claim that models like **Claude Opus 4.6** are “bad at UI”. In most cases, the model isn’t the real problem, the **prompt is**. The user doesn’t know how to describe what they want, the model fills in the blanks with its standard style, and the final result feels generic. The model that gets labeled as “good at UI” is often just the one whose defaults happen to align with what the user had in mind.

### What I recommend doing

To get out of this generic zone, you need to **treat frontend generation like any other engineering task**: you need a clear, detailed spec. This is even more important if you don’t work with frontend.

A few simple, practical recommendations:

* **Use a different font.**
  Avoid the usual pattern of always using the same safe fonts that every LLM suggests by default. This small change already helps break the “LLM look”.

* **Do not add emojis.**
  Emojis tend to make the design feel even more like a templated LLM output. If your goal is a more professional or distinctive interface, they usually hurt more than they help.

* **Understand that, by default, the model will drift back to its “average” UI.**
  If you don’t give strong constraints or clear preferences, the result will usually be a familiar, bland layout with the same common patterns repeated.

### Practical tips to get better frontend results

#### 1. Use screenshots of designs you like

You might not know the right words, but the model can infer a lot from images. In this context, a screenshot really is worth more than a long written description.

Some good sources for UI inspiration:

* Behance
* Dribbble
* Mobbin (paid, but worth it if you care a lot about product design)

When prompting, you can do something like: “Use this screenshot as a visual reference for layout and structure, but adapt it to my use case.” That way, you don’t need perfect design vocabulary to communicate what you want.

#### 2. Ask for proposals before committing to a final design

Instead of asking directly for “the final UI”, first ask for **multiple design directions**. For example: three distinct layout concepts or two very different visual styles.

This does two things:

1. It “seeds” different paths early on, making it much less likely that everything will look the same.
2. It gives you something to react to, you can say “combine layout from option A with the color scheme from option B”, which is often easier than starting from a blank slate.

Don’t be afraid to go back and forth. Good frontend often comes from **iteration**, not from the first attempt.

#### 3. Explicitly ban common defaults and tendencies

LLMs have a set of visual habits they fall back to over and over again. If you want something less generic, it helps to **block some of these habits in your prompt**.

Some defaults I recommend explicitly banning:

* No **Inter** or **Roboto**
* No **shadcn** (controversial, but worth considering if you want to avoid the “every Tailwind/React app looks the same” problem)
* No **gradients**
* No **emojis**

You don’t have to ban all of these forever, but including these constraints forces the model to think a bit more and step outside the most obvious choices.

#### 4. Tell the model to make bold decisions, not safe ones

Under the hood, LLMs tend to learn **conservative** design choices through reinforcement learning and fine-tuning. The result is a visual style that’s “fine” and “reasonable”, but also **visually boring**.

If you want something that actually stands out, you need to push the model away from that conservative center. In your prompt, make it clear that you:

* Prefer a **strong, memorable design** over a perfectly “safe” one
* Are comfortable with **bold choices** in color, layout, or typography
* Want the model to **take risks** and avoid corporate-looking templates

For example, you can say: “Avoid safe, corporate UI. I’d rather something strong and opinionated, even if it’s not perfect, than something generic.”

---

## Rule 2 – Code Quality and Best Practices

**From what I’ve seen**, LLMs are not capable of writing truly clean code on their own. When creating your prompt, I suggest explicitly instructing the LLM to generate the project following **Clean Code best practices** and proper **design principles**.

However, **it’s important to understand** that following Clean Code principles often involves trade-offs. You may lose performance in favor of readability and maintainability. Clean Code should not be viewed as a set of absolute rules that must always be followed. It’s up to each developer to decide which best practices are worth adopting for their specific context.

**In my opinion**, you must already have some coding knowledge and understand Clean Code best practices to guide the LLM effectively. This knowledge allows you to specify which practices the LLM should follow when generating code. No LLM I’ve tested truly understands how to produce readable, well-structured code on its own without explicit guidance.

**My recommendation**: Use **Claude** to help you create prompts that clearly specify which Clean Code practices you want to follow. This can significantly improve the readability of the generated code while preserving the trade-offs you’re willing to accept.

---

## Rule 3 – Prompt Generation Limitations

**Based on my tests**, LLMs are generally not capable of generating high-quality prompts on their own, with the notable exception of **Claude**.

I believe this is because Anthropic (the company behind Claude) released official documentation explaining how to write effective prompts. As a result, Claude has internal knowledge that helps it generate better prompts and meta-prompts.

However, this does **not** mean that Claude inherently understands all best practices of prompt engineering, at least not in my experience. You still need to review, adapt, and often refine what it suggests.

---

## Rule 4 – Limitations with Complex Programs

**In my experience**, you should not attempt to generate complex programs with LLMs if you don’t already have a solid foundation. I’ve found that LLMs still struggle with deeper logical reasoning and are not able to properly think through complex or advanced tasks end-to-end.

If you decide to generate code for a complex program, I strongly recommend including **external sources** in the project: documentation, architecture diagrams, example repositories, RFCs, and so on. The more references you provide, the better. This allows the LLM to anchor its output on concrete materials you supply instead of hallucinating structure and details.

---

## Rule 5 – Recommended LLM for Coding

**As of my last testing** (February 2026), these are the LLMs I have tested the most and therefore have the most experience with:

* **Claude Opus 4.6**
* **Codex 5.3**

### Claude Opus 4.6

Released on **February 17, 2026**, the launch generated some controversy, many developers were expecting the release of Sonnet 5 instead. Shortly after launch, several developers commented that the new version felt less capable than its predecessor (Opus 4.5). Over time, that perception seems to have shifted, and currently Opus 4.6 is regarded as the **best model for coding tasks** in my experience.

The closest competitor today is **Codex 5.3**, a new model from OpenAI, which is the only model that comes close to matching Opus 4.6 in overall coding quality.

**In my opinion**, for serious development work, Opus 4.6 is still the clear choice.

---

## Rule 5.1 – Other LLMs and Their Use Cases

While I only recommend **Claude Opus 4.6** for actual coding, other models can still be useful for specific tasks.

### Claude Sonnet 4.6

Released on **February 17, 2026**, I haven’t tested it extensively, but from the few tests I’ve done, it has been impressively capable. It has become my go-to replacement for GPT 5.2 in certain scenarios.

For example, when I had problems configuring files, IDEs, or text editors, I used to ask GPT 5.2, but it often gave nonsensical answers and failed to help even after multiple attempts. A specific case: I was trying to make Zed automatically run `gopls` to format my `.go` files on save. GPT 5.2 couldn’t solve it after many tries; Sonnet 4.6 resolved it quickly.

### Gemini 3.1 Pro

Released on **February 19, 2026**, the most noticeable change from Gemini 3 Pro to 3.1 Pro is **speed**, and not in a good way. The new version is significantly slower than any model I’ve used before, making it practically unusable in my workflow (tested within Antigravity).

### Gemini 3 Flash

**In my opinion**, Gemini 3 Flash is not suitable for coding tasks.
However, it is the **fastest and cheapest** option available right now.

**Important strength**: Gemini 3 Flash is very good at extracting information or content from text. It’s smart enough to handle this task effectively and does so extremely quickly.

I’ve found that you can build a decent UI with it, but I don’t recommend using it for debugging if UI errors occur. Based on my experience, Gemini 3 Flash is best suited for **quickly checking or verifying information** due to its speed.

**Important Note on Hallucination**: Gemini 3 Flash and Pro models require more careful prompting than models like Claude Opus 4.6. According to benchmark data, Gemini 3 Flash scores 91% on hallucination tests while Gemini 3 Pro scores 88%, indicating they need more attention when crafting prompts.

One technique that has worked well for me, inspired by Anthropic’s leaked Claude system prompt, is to structure prompts so that **more than 80% of the text consists of rules about what the model should NOT do**. This helps funnel the model away from incorrect paths and reduces hallucinations.

I suggest avoiding Gemini 3 Flash for complex content generation, except for **UI/GUI tasks and text extraction**.

<img width="1572" height="617" alt="image" src="https://github.com/user-attachments/assets/837637e1-c253-4721-be03-e5749d3ece13" />
<img width="2372" height="1024" alt="image" src="https://github.com/user-attachments/assets/bf982b43-12f8-41ac-ab3f-f3b028d566ed" />

---

### Gemini 3 Pro

**From my testing**, Gemini 3 Pro is also not recommended for coding.
It is, however, very effective for building UIs, similar to Gemini 3 Flash.

The Pro version, in my experience, is **smarter and significantly more expensive**, which makes it suitable for debugging UI/GUI issues. I don’t recommend using it to generate complex, logic-heavy content.

**Important Note on Hallucination**: You need to be even more careful with how you phrase prompts to Gemini 3 Pro than with a more reliable model like Claude Opus 4.6. As mentioned above, following the prompt-engineering technique derived from Anthropic’s leaked system prompt (80% rules about what NOT to do) is particularly effective with this model.

**Important Note**: Gemini 3 Pro is noticeably superior compared to Flash for tasks outside UI. While both models perform similarly for UI design, the Pro version shows significantly better performance in **analysis, verification, and text processing**.

In my workflow, I’ve found it best used for **analysis and verification**.

---

### GLM 5

Released on **February 11, 2026**, **GLM 5** is a Chinese open-source model and represents a significant leap forward for open-source generative AI. While it still falls behind the best proprietary coding models (currently Opus 4.6 and Codex 5.3), I found it very interesting for **conversational use**.

After using it extensively, I realized it can be highly valuable for **discussing a project, exploring ideas, or any longer conversation**, especially because it’s free. In those cases, I found it a better option than using GPT 5.2, which I would otherwise reach for.

---

### Kimi k2.5

Released on **January 26, 2026**, **Kimi k2.5** is another Chinese open-source model. At the time of its release (before GLM 5), it was the best open-source model available, especially for coding. However, as of February 2026, I don’t see many reasons to keep using it.

In my opinion, it’s more effective to simply use **Claude Sonnet 4.6**, and since it’s free (within daily limits), you can rotate between Google accounts when you hit the limit if you really need more usage.

---

## Rule 6 – Python as an Exception

Rule 4 has some important exceptions, especially when working with **Python**, at least from what I’ve observed.

**In my view**, Python is a unique language. It’s common, especially in universities or online discussions, to hear claims that Python will eventually be replaced, just like COBOL, Fortran, Lisp, BASIC, Pascal, and others. I believe this claim is incorrect.

**From my understanding**, programming languages are not replaced without valid reasons. Older languages declined because they were no longer competitive in the market or didn’t adapt well to new use cases. Python, on the other hand, is one of the most **flexible** programming languages available and one of the **simplest to learn**.

Python is widely used for:

* Process automation
* Data analysis
* Machine learning
* Data science

**I believe** this is why LLMs rely so heavily on Python for benchmarks, especially those related to math and reasoning. I’ve also noticed that many LLMs tend to use Python when generating scripts for PDFs, DOCX files, and other automation tasks.

As a result, Python is the programming language that LLMs are **most proficient in**. Even the free version of ChatGPT can help you create Python scripts effectively, as long as you’re able to review and adjust the logic when necessary.

---

## Rule 7 – IDEs, Tooling, and User Knowledge Matter

LLM performance can vary a lot depending on the **IDE or tool** you’re using. Some companies deliberately limit model capabilities to reduce costs, while others don’t invest in strong system prompts or proper configuration for their integrations.

This is why, in certain IDEs like Antigravity (Google’s AI-powered IDE), **Claude Opus 4.6 can feel noticeably weaker** compared to how it performs in tools like Cursor. The difference is not the model itself, but how it’s configured, constrained, and prompted by the platform.

**In my view**, if you don’t understand what computing and mathematics can actually do, and how to apply them, you won’t know how to ask the right questions to an LLM. As a result, you will consistently generate simple, limited applications with poor optimization and multiple security gaps.

You don’t know what you don’t know. **I believe** only people who truly understand a subject know how to ask the right questions about it.

**My analogy**: This is similar to gastronomy. If you only know how to cook an egg, you will always cook eggs, no matter how good the kitchen tools are.

---

## Final Note

These observations are based on my personal workflow and the specific contexts in which I use LLMs. Your experience may be completely different, and that’s expected.

I strongly encourage you to test, explore, and form your own conclusions about what works best for your use cases. Use this document as a set of **personal notes**, not absolute truths.
