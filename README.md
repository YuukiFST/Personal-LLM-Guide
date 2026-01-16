# Practical Guide to Using LLMs - Personal Experiences

> **Important Notice**: This document reflects my personal experiences and opinions based on practical use of different LLMs over time. The observations described here may not apply to all use cases and may vary depending on context, tools used, and model evolution.

This guide contains observations that I have not found in other official documentation. I refer to the numbered items below as **"rules"** to facilitate cross-references.

**Last update of my experiences**: January 2026

---

## Rule 1 – UI Design and LLM Behavior

**In my experience**, the best LLMs for UI design are **Gemini 3 Pro** and **Gemini 3 Flash**.  
However, I've noticed they tend to generate very similar UIs about 90% of the time. In my observation, anyone familiar with LLM outputs will recognize that the design follows a specific **"vibe coding"** style.

### What I recommend doing

- Use a different font  
- Do not add emojis

---

## Rule 2 – Code Quality and Best Practices

**From what I've seen**, LLMs are not capable of writing clean code on their own. When creating your prompt, I suggest explicitly instructing the LLM to generate the project following **Clean Code best practices** and proper **design principles**.

However, **it's important to understand** that following Clean Code principles often involves trade-offs. You may lose performance in favor of readability and maintainability. Clean Code should not be viewed as absolute rules. It's up to each developer to decide which best practices they believe are worth adopting for their specific context.

**In my opinion**, you must already have coding knowledge and understand clean code best practices to effectively guide the LLM. This knowledge allows you to specify which practices the LLM should follow when generating code. No LLM I've tested truly understands how to produce readable code on its own without explicit guidance.

**My recommendation**: Use Claude to help you create prompts that clearly specify which clean code practices you want to follow. This can significantly improve the readability of the generated code while maintaining the trade-offs you're willing to accept.

---

## Rule 3 – Prompt Generation Limitations

**Based on my tests**, LLMs are generally not capable of generating high-quality prompts on their own, with the exception of **Claude**.

I believe this is because Anthropic (the company behind Claude) released official documentation explaining how to write effective prompts. As a result, Claude has internal knowledge that helps it generate better prompts.

However, this does **not** mean that Claude inherently understands all best practices of prompt engineering—at least not in my experience.

---

## Rule 4 – Limitations with Complex Programs

**In my experience**, you should not attempt to generate complex programs without a solid foundation. I've found that LLMs lack strong logical reasoning and are not capable of properly thinking through complex or advanced tasks.

If you decide to generate code for a complex program, I recommend including **external sources** in the project. The more references you provide, the better. This allows the LLM to base its output on the materials you supply.

---

## Rule 5 – Recommended LLMs by Use Case

**As of my last testing** (January 2026), the best LLMs I've found to help with projects are:

- **Gemini 3 Flash**
- **Gemini 3 Pro**
- **Claude Sonnet 4.5**
- **Claude Opus 4.5**

### Gemini 3 Flash

**In my opinion**, the worst option for coding among the models mentioned.  
However, it is the **fastest and cheapest** option.

I've found you can build a good-looking UI with it, but I don't recommend using it for debugging if UI errors occur. Based on my experience, Gemini 3 Flash is best suited for quickly checking or verifying information due to its speed.

I suggest avoiding it for complex content generation, except for UI/GUI tasks.

---

### Gemini 3 Pro

**From my testing**, the second worst option for coding.  
It is effective for building UI, similar to Gemini 3 Flash.

The Pro version, in my experience, is smarter and significantly more expensive, which makes it suitable for debugging UI/GUI issues. I don't recommend using it to generate complex logic-heavy content.

I've found it is best used for **analysis and verification** purposes.

---

### Claude Sonnet 4.5

**In my opinion**, one of the best options for coding among the models mentioned.  
I've found it capable of producing high-quality code when given precise and well-structured prompts.

My recommendation is to be very specific in your prompts to obtain the best results.

---

### Claude Opus 4.5

**Based on my experience**, the best option for coding as of **January 2026**, and also the most expensive model.

---

## Rule 6 – Python as an Exception

Rule 4 has some exceptions, especially when working with **Python**—at least from what I've observed.

**In my view**, Python is a unique language. It is common—especially in universities—to hear claims that Python will eventually be replaced, like COBOL, Fortran, Lisp, BASIC, Pascal, and others. I believe this claim is incorrect.

**From my understanding**, programming languages are not replaced without valid reasons. The older languages declined because they were no longer competitive in the market. Python, on the other hand, is one of the most flexible programming languages available and also one of the simplest to learn.

Python is widely used for:

- Process automation  
- Data analysis  
- Machine learning  
- Data science  

**I believe** this is why LLMs rely heavily on Python for benchmarks, especially math-related tasks. Additionally, I've noticed LLMs use Python to generate PDFs, DOCX files, and other formats.

**In my experience**, Python is the programming language that LLMs are most proficient in. As a result, even the free version of ChatGPT can effectively help you create Python scripts.

---

## Rule 7 – IDEs, Tooling, and User Knowledge Matter

**I've observed that** LLM performance can vary significantly depending on the IDE or tool being used. Some companies, in my opinion, deliberately limit model capabilities to reduce costs, while others fail to use high-quality system prompts for their LLM integrations.

This is why, **based on my testing**, in some IDEs, such as Antigravity, **Claude Opus 4.5 may appear weaker** compared to its performance in tools like Cursor. I believe the difference is not necessarily the model itself, but how it is configured, constrained, and prompted.

**In my view**, if you do not understand what computing and mathematics are capable of—or how to apply them—you will not know how to ask the LLM the right questions. As a result, you will consistently generate simple, limited applications with poor optimization and multiple security gaps.

You do not know what you do not know. **I believe** only those who truly understand a subject know how to ask the right questions.

**My analogy**: This is similar to gastronomy—if you only know how to cook an egg, you will always cook eggs, no matter how good the kitchen tools are.

---

## Final Note

These observations are based on my personal workflow and the specific contexts in which I use LLMs. Your experience may differ. I encourage you to test and form your own conclusions about what works best for your use cases.
