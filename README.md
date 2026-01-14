# My Documentation about LLMs

I will not include information here that is already present in other documents, whether from other developers or AI companies.  
I will only include information that I have not found in any other documentation.  
I will refer to the numbered items below as **“rules”**, so I can reference them in other rules.

---

## Rule 1 – UI Design and LLM Behavior

The best LLMs for UI design are **Gemini 3 Pro** and **Gemini 3 Flash**.  
However, they tend to generate almost the same UI about 90% of the time. Anyone who truly understands LLM outputs will recognize that the design is based on a specific **“vibe coding”** style.

### What you need to do

- Use a different font  
- Do not add emojis

---

## Rule 2 – Code Quality and Best Practices

LLMs are not capable of writing clean code on their own. When creating your prompt, you should explicitly instruct the LLM to generate the project following **Clean Code best practices** and proper **design principles**.

You must already have coding knowledge to do this effectively, because no LLM truly understands how to produce readable, minimalist code without compromising performance.

---

## Rule 3 – Prompt Generation Limitations

LLMs are generally not capable of generating high-quality prompts on their own, with the exception of **Claude**.

This is because Anthropic (the company behind Claude) released official documentation explaining how to write effective prompts. As a result, Claude has internal knowledge that helps it generate better prompts.

However, this does **not** mean that Claude inherently understands all best practices of prompt engineering.

---

## Rule 4 – Limitations with Complex Programs

Do not attempt to generate complex programs without a solid foundation. LLMs lack strong logical reasoning and are not capable of properly thinking through complex or advanced tasks.

If you decide to generate code for a complex program, you should include **external sources** in the project. The more references you provide, the better. This allows the LLM to base its output on the materials you supply.

---

## Rule 5 – Recommended LLMs by Use Case

As of today, the best LLMs to help you with projects are:

- **Gemini 3 Flash**
- **Gemini 3 Pro**
- **Claude Sonnet 4.5**
- **Claude Opus 4.5**

### Gemini 3 Flash

The worst option for coding among the models mentioned.  
However, it is the **fastest and cheapest** option.

You can build a good-looking UI with it, but do not use it for debugging if UI errors occur. Gemini 3 Flash is best suited for quickly checking or verifying information due to its speed.

Avoid using it for complex content generation, except for UI/GUI tasks.

---

### Gemini 3 Pro

The second worst option for coding.  
It is effective for building UI, similar to Gemini 3 Flash.

The Pro version is smarter and significantly more expensive, which makes it suitable for debugging UI/GUI issues. Do not use it to generate complex logic-heavy content.

It is best used for **analysis and verification** purposes.

---

### Claude Sonnet 4.5

One of the best options for coding among the models mentioned.  
It is capable of producing high-quality code when given precise and well-structured prompts.

Be very specific in your prompts to obtain the best results.

---

### Claude Opus 4.5

The best option for coding as of today (**January 8, 2026**), and also the most expensive model.

---

## Rule 6 – Python as an Exception

Rule 4 has some exceptions, especially when working with **Python**.

Python is a unique language. It is common—especially in universities—to hear claims that Python will eventually be replaced, like COBOL, Fortran, Lisp, BASIC, Pascal, and others. This claim is incorrect.

Programming languages are not replaced without valid reasons. The older languages declined because they were no longer competitive in the market. Python, on the other hand, is one of the most flexible programming languages available and also one of the simplest to learn.

Python is widely used for:

- Process automation  
- Data analysis  
- Machine learning  
- Data science  

This is why LLMs rely heavily on Python for benchmarks, especially math-related tasks. Additionally, LLMs use Python to generate PDFs, DOCX files, and other formats.

Python is the programming language that LLMs are most proficient in. As a result, even the free version of ChatGPT can effectively help you create Python scripts.

---

## Rule 7 – IDEs, Tooling, and User Knowledge Matter

LLM performance can vary significantly depending on the IDE or tool being used. Some companies deliberately limit model capabilities to reduce costs, while others fail to use high-quality system prompts for their LLM integrations.

This is why, in some IDEs, such as Antigravity, **Claude Opus 4.5 may appear weaker** compared to its performance in tools like Cursor. The difference is not necessarily the model itself, but how it is configured, constrained, and prompted.

If you do not understand what computing and mathematics are capable of—or how to apply them—you will not know how to ask the LLM the right questions. As a result, you will consistently generate simple, limited applications with poor optimization and multiple security gaps.

You do not know what you do not know. Only those who truly understand a subject know how to ask the right questions.

This is similar to gastronomy: if you only know how to cook an egg, you will always cook eggs—no matter how good the kitchen tools are.
