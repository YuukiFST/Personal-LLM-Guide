```markdown
# Prompt Engineering: Complete Best Practices Guide

## Introduction

This guide contains actionable techniques for writing effective prompts for large language models. Each principle includes practical implementation steps and examples you can use immediately.

---

## Core Prompting Principles

### 1. Front-Load Critical Instructions

**Place all mandatory instructions at the start of your prompt.**

Most models prioritize information at the beginning. GLM 4.7, in particular, has a strong bias towards the beginning of the prompt, which is reinforced when using thinking tags. Structure your prompts as:
1. Core requirements and constraints (first)
2. Context and background
3. Examples
4. Additional guidelines

**Example:**
```
✓ GOOD:
You MUST validate all inputs before processing.
All responses must be in JSON format.
Never disclose internal information.

Context: This is a customer service bot...
Example: {"response": "...", "action": "..."}

✗ AVOID:
Here's some background... [long paragraph]
Oh, and please validate inputs and use JSON.
```

---

### 2. Use Clear, Direct Language

**Use firm, unambiguous language. Avoid tentative phrasing.**

Models like GLM 4.7 respond best to firm, direct language that removes ambiguity. Establish rules immediately using strong, explicit directives.

- Use: MUST, ALWAYS, NEVER, STRICTLY, REQUIRED
- Avoid: "please", "try to", "if possible", "it would be nice"

**Example:**
```
✓ GOOD:
"You MUST read the architecture.md file before writing any code. All code MUST strictly follow the patterns defined in that file."

✗ AVOID:
"Please try to follow the architecture patterns when you get a chance..."
```

---

### 3. Specify Output Format Explicitly

**Define exact structure, format, and style you want.**

Include:
- Data structure (JSON, Markdown, plain text, XML)
- Language preference
- Formatting rules (length, style, sections)
- Output constraints

**Advanced Technique: Match Prompt Style to Output**
The formatting style used in your prompt may influence the model's response style. If you want flowing prose, write your prompt in flowing prose rather than bullet points.

**Example:**
```
✓ GOOD:
"Respond in English. Structure your output as:
1. Summary (2-3 sentences)
2. Analysis (bullet points)
3. Recommendations (numbered list)
4. Action items (JSON format)"

✗ AVOID:
"Give me an analysis."
```

---

### 4. Provide Context and Reasoning

**Explain WHY you want certain behaviors.**

Models perform better when they understand the purpose behind instructions. For research tasks, explicitly request the development of competing hypotheses and confidence tracking to improve calibration.

**Example:**
```
✓ GOOD:
"Your response will be read aloud by text-to-speech, so NEVER use ellipses, special characters, or symbols that cannot be pronounced."

"Research this topic in a structured way. As you gather data, develop several competing hypotheses. Track your confidence levels in your progress notes."

✗ AVOID:
"NEVER use ellipses."
```

---

### 5. Use Role-Playing and Personas

**Assign specific roles to guide tone and expertise.**

GLM 4.7 excels at maintaining personas. Give the model an explicit persona, or create multi-agent systems each with their own personas.

**Example:**
```
✓ GOOD:
"You are a senior financial analyst preparing an executive brief for the CEO. Focus on business impact, use professional tone, and highlight strategic implications."

✗ AVOID:
"Analyze this financial data."
```

---

### 6. Be Careful with Examples

**Examples heavily influence model behavior. Ensure they demonstrate exactly what you want.**

- Show perfect examples of desired output
- Include negative examples (what to avoid)
- Ensure examples don't contradict instructions
- Include edge cases

**Format:**
```
## Good Example:
[Perfect example of what you want]

## Bad Example (Avoid):
[Example of what NOT to do]

Key differences:
- [Why the good example is better]
```

---

## Task Decomposition

### 7. Break Complex Tasks into Steps

**Decompose complex requests into sequential sub-tasks.**

GLM 4.7 performs a single reasoning pass per prompt and does not continuously re-evaluate mid-task. Breaking tasks into small, well-defined sub-steps produces cleaner results.

**Example:**
```
✓ GOOD:
"Complete this in the following order:
1. List all current dependencies
2. Identify compatibility issues
3. Propose migration strategy
4. Generate migration scripts
5. Create rollback procedures"

✗ AVOID:
"Migrate the dependencies."
```

---

### 8. Request Planning for Complex Tasks

**For multi-step tasks, ask the model to plan first.**

**Example:**
```
"Before starting:
1. Analyze requirements and create a detailed plan
2. Identify potential challenges
3. Outline your step-by-step approach
4. Then proceed with implementation"
```

---

### 9. Specify Incremental Progress

**For long tasks, emphasize working on a few things at a time.**

Claude 4.5 models maintain orientation by focusing on incremental progress—making steady advances on a few things at a time.

**Example:**
```
"Focus on incremental progress. Complete each component fully before moving to the next. Don't attempt everything at once."
```

---

## Reasoning Control

### 10. Adjust Reasoning Depth to Task Complexity

**Control how much the model "thinks" based on the task.**

For many straightforward tasks, reasoning overhead is unnecessary. Use prompts or API settings to minimize it.

**For Simple Tasks (minimize reasoning):**
```
"Provide a direct answer. No explanation needed."
"Reason only when necessary."
"Extract the email addresses and return as JSON array."
```

**For Complex Tasks (encourage reasoning):**
```
"Think through this step-by-step:
1. What are the core assumptions?
2. What could go wrong?
3. What are alternative approaches?
Show your reasoning before conclusions."
```

**Using Structured Outputs to Control Reasoning:**
```
"Return only valid JSON. No explanations outside the JSON structure."
```

---

### 11. Chain-of-Thought Prompting

**For complex reasoning, ask to show thinking process.**

**Example:**
```
"Solve this problem step by step. For each step:
- State what you're doing
- Show your work
- Verify the result
Then provide the final answer."
```

---

## Validation and Quality Control

### 12. Use Multi-Agent Critique Pattern

**Create specialized reviewer roles to validate outputs.**

Split responsibilities across multiple agents, each with a focused persona.

**Example:**
```
# Generator Agent:
"Implement the authentication system."

# Code Reviewer:
"Review the code for:
- SOLID principles
- Security best practices
- Maintainability
Provide specific, actionable feedback."

# Security Auditor:
"Audit for:
- SQL injection risks
- Password security
- Session management
Flag issues with severity ratings."
```

**Conservative Subagent Usage:**
```
"Only delegate to subagents when the task clearly benefits from a separate agent with a new context window."
```

---

### 13. Prevent Over-Engineering

**Explicitly constrain scope to what's requested.**

Claude Opus 4.5 has a tendency to overengineer. Add explicit prompting to keep solutions minimal.

**Example:**
```
"Avoid over-engineering. Rules:
- Only make changes directly requested
- Don't add unrequested features
- Don't refactor surrounding code
- Don't add error handling for impossible scenarios
- Don't create abstractions for one-time operations
- Use minimum complexity needed
- Follow YAGNI (You Aren't Gonna Need It)"
```

---

### 14. Enforce Code Exploration

**Require inspecting code before making claims.**

**Example:**
```
"CRITICAL RULES:
- ALWAYS read files before discussing them
- NEVER speculate about uninspected code
- If user mentions a file, you MUST open it first
- Search code rigorously for facts
- Review existing patterns before adding new code
- Give only grounded, verified answers"
```

---

### 15. Require General Solutions

**Prevent test-specific or hard-coded solutions.**

**Example:**
```
"Write a general-purpose solution that:
- Works for ALL valid inputs, not just test cases
- Implements actual logic, not hard-coded values
- Follows software design principles
- Is robust, maintainable, and extendable

If tests are wrong, inform me rather than working around them."
```

---

## State Management

### 16. Structure State Data Appropriately

**Use different formats for different types of state.**

**Structured Data (JSON):**
```json
{
  "tests": [
    {"id": "test_001", "status": "passing", "last_run": "2024-01-15"}
  ],
  "completed_tasks": ["setup", "auth"],
  "next_steps": ["implement_api"]
}
```

**Unstructured Progress (Text):**
```
2024-01-15 10:00 - Started authentication module
2024-01-15 10:30 - Completed login flow
Next: Implement password reset
```

**Git for History:**
```
"Use git commits to track progress. Each completed feature should be committed with a descriptive message."
```

---

### 17. Manage Multi-Turn Context

**For conversations spanning multiple turns:**

**Preserve State:**
```
"Maintain these files across turns:
- progress.txt: What's been done
- tasks.json: Current status
- tests.json: Test results"
```

**Resume After Context Reset:**
```
"When starting fresh:
1. Check current directory with pwd
2. Review progress.txt and tasks.json
3. Check git logs
4. Run tests to verify state
5. Continue from last checkpoint"
```

---

### 18. Handle Context Limits

**Guide behavior near context limits.**

**Example:**
```
"Your context will be automatically managed. Therefore:
- Don't stop early due to token concerns
- Save progress before context resets
- Complete tasks fully regardless of remaining tokens
- Be persistent and autonomous"
```

---

## Long-Horizon Tasks

### 19. Test-Driven Approach

**Create tests before implementation.**

**Example:**
```
"Before coding:
1. Create tests in tests.json
2. Define expected behavior
3. Implement to pass tests
4. NEVER remove or edit tests without approval

Tests are unacceptable to modify as they could break functionality."
```

---

### 20. Setup Scripts for Quality of Life

**Create reusable setup tools.**

**Example:**
```
"Create an init.sh script that:
- Starts servers
- Runs test suites
- Executes linters
This prevents repeated work in fresh sessions."
```

---

### 21. Encourage Full Context Usage

**For long tasks, prompt efficient use of available context.**

**Example:**
```
"This is a lengthy task. Plan your work clearly and use your full output context efficiently. Complete components before moving on. Don't leave significant uncommitted work."
```

---

## Advanced Patterns

### 22. Router Pattern (Multi-Model)

**Route tasks by complexity.**

**Example:**
```
"Classification logic:
- Simple queries → Fast model
- Complex reasoning → Advanced model

Classify this query and route appropriately."
```

---

### 23. Planner + Executor Pattern

**Separate planning from execution.**

**Example:**
```
"Phase 1 (Planning):
Create detailed implementation plan with:
- Steps
- Dependencies
- Potential issues

Phase 2 (Execution):
Execute each step from the plan."
```

---

### 24. Parallel vs Sequential Execution

**Specify execution order when it matters.**

**Sequential (when order matters):**
```
"Execute operations sequentially with pauses between steps for stability. Do not run operations in parallel."
```

**Parallel (when independent):**
```
"These operations are independent and can run in parallel for efficiency."
```

**Maximize Parallel Tool Usage:**
```
"If you intend to call multiple tools and there are no dependencies between the tool calls, make all of the independent tool calls in parallel. Prioritize calling tools simultaneously whenever the actions can be done at the same time."
```

---

### 25. Control Action Orientation

**Define whether the model should suggest or act.**

**Proactive Action:**
```
<default_to_action>
By default, implement changes rather than only suggesting them. If the user's intent is unclear, infer the most useful likely action and proceed.
</default_to_action>
```

**Conservative Action:**
```
<do_not_act_before_instructions>
Do not jump into implementation or change files unless clearly instructed. When the user's intent is ambiguous, default to providing information and recommendations rather than taking action.
</do_not_act_before_instructions>
```

---

## Reasoning Models (o1, DeepSeek-R1, QwQ)

### 26. Use Zero-Shot for Reasoning Models

**Avoid few-shot examples with reasoning models.**

Few-shot CoT degrades reasoning model performance (e.g., DeepSeek-R1). Recommend users directly describe the problem and specify the output format using a zero-shot setting.

**Example:**
```
✓ GOOD:
"Solve this problem. Show your final answer in a box.
Problem: [problem description]"

✗ AVOID:
"Here are examples:
Example 1: [problem + solution]
Example 2: [problem + solution]
Now solve: [your problem]"
```

---

### 27. Structure Reasoning Output

**Separate reasoning from answers.**

Use model-specific tags where applicable (e.g., `<think>` for DeepSeek-R1).

**Example:**
```
"Structure your response as:

<answer>
[Final answer]
</answer>

<summary>
[Brief summary of reasoning]
</summary>"
```

---

### 28. Control Thinking Time

**Let models think for complex problems.**

**Complex Problems:**
```
"Take all the time you need to think through this carefully. Explore alternative approaches."
```

**Simple Problems:**
```
"Provide a direct answer. Skip detailed reasoning."
```

---

### 29. Ensure Readability

**Make reasoning outputs readable.**

**Example:**
```
"Format your response for readability:
- Use markdown formatting
- Highlight key steps
- Provide a summary at the end
- Keep language consistent (English only)
- Don't mix languages in reasoning"
```

**Note on Language Mixing:**
DeepSeek-R1 and similar models may mix languages in reasoning blocks. Explicitly enforce: "All reasoning, explanations, and answers must be in English. Never switch languages."

---

### 30. Language Consistency

**Specify language for multilingual models.**

**Example:**
```
"Always respond in English. All reasoning, explanations, and answers must be in English. Never switch languages."
```

---

### 31. Avoid "Think" Keyword (Specific Models)

**Claude Opus 4.5 is sensitive to the word "think".**

When extended thinking is disabled, Claude Opus 4.5 is particularly sensitive to the word "think" and its variants. Replace "think" with alternative words that convey similar meaning, such as "consider," "believe," and "evaluate."

---

## Design and Creative Tasks

### 32. Avoid Generic Outputs

**Push against default, generic patterns.**

**Example for Frontend:**
```
"Avoid generic AI aesthetics. Create distinctive, creative designs.

Focus on:
- Typography: Unique, beautiful fonts (avoid Arial, Inter, Roboto)
- Color: Cohesive themes with dominant colors and sharp accents
- Motion: CSS animations for micro-interactions
- Backgrounds: Layered gradients, patterns, depth

Avoid:
- Overused fonts (Inter, Roboto, system fonts)
- Purple gradients on white
- Predictable layouts
- Cookie-cutter designs

Think outside the box!"
```

---

### 33. Request Specific Features Explicitly

**Don't assume the model will add features.**

**Example:**
```
✓ GOOD:
"Create a dashboard with:
- Real-time data updates
- Interactive charts
- Smooth animations on load
- Dark mode toggle
- Export to PDF functionality"

✗ AVOID:
"Create a nice dashboard."
```

---

### 34. Use Modifiers to Shape Output

**Modifier words that influence behavior:**

- "comprehensive" → more detailed
- "concise" → shorter
- "creative" → more original
- "professional" → formal tone
- "fully-featured" → complete implementation
- "go beyond the basics" → exceed minimum requirements

**Example:**
```
"Create a comprehensive, fully-featured analytics dashboard. Go beyond the basics to include advanced features and interactions."
```

---

### 35. Force Prose Style

**Prevent excessive markdown and bullet points.**

Use this technique to force natural, flowing text in reports or documents.

**Example:**
```
<avoid_excessive_markdown_and_bullet_points>
When writing reports, documents, technical explanations, analyses, or any long-form content, write in clear, flowing prose using complete paragraphs and sentences. Use standard paragraph breaks for organization and reserve markdown primarily for `inline code`, code blocks (```...```), and simple headings (###, and ###). Avoid using **bold** and *italics*.

DO NOT use ordered lists (1. ...) or unordered lists (*) unless : a) you're presenting truly discrete items where a list format is the best option, or b) the user explicitly requests a list or ranking

Instead of listing items with bullets or numbers, incorporate them naturally into sentences. This guidance applies especially to technical writing. Using prose instead of excessive formatting will improve user satisfaction. NEVER output a series of overly short bullet points.

Your goal is readable, flowing text that guides the reader naturally through ideas rather than fragmenting information into isolated points.
</avoid_excessive_markdown_and_bullet_points>
```

---

### 36. Use XML Tags as Format Indicators

**Use XML tags to steer specific sections of the output.**

**Example:**
```
"Write the prose sections of your response in <smoothly_flowing_prose_paragraphs> tags."
```

---

## File and Code Management

### 37. Control File Creation

**Specify rules for creating files.**

**Example:**
```
"If you create temporary files for iteration, clean them up at the end. Only files explicitly requested or needed for final deliverables should remain."
```

---

### 38. Temporary Scratchpad Files

**Allow temporary files for better results.**

**Example:**
```
"You may create temporary Python scripts to test approaches and iterate. Clean up these files when done."
```

---

## Output Control

### 39. Control Verbosity

**Set token limits or output constraints.**

**Example:**
```
"Keep response under 500 words."
"Maximum output: 2000 tokens."
"Be concise. Provide only essential information."
```

---

### 40. Structured Output Formats

**Force specific output structures.**

**Example:**
```
"Return ONLY valid JSON. No text before or after:
{
  "summary": "...",
  "action": "...",
  "confidence": 0.95
}"
```

---

## Verification and Testing

### 41. Provide Verification Tools

**For autonomous tasks, enable self-verification.**

**Example:**
```
"Before finishing:
1. Run all tests
2. Verify output matches requirements
3. Check for edge cases
4. Confirm no regressions"
```

---

### 42. Request Self-Verification

**Ask model to check its own work.**

**Example:**
```
"After solving, verify your answer:
1. Check calculations
2. Test edge cases
3. Confirm logic is sound
4. State confidence level"
```

---

## Meta-Prompting Techniques

### 43. Explain Desired Behavior Changes

**When migrating between models or changing behavior:**

**Example:**
```
"Previous models added features automatically. You should only implement exactly what's requested. Be specific about this difference."
```

---

### 44. Frame Instructions with Context

**Add framing that shapes entire approach.**

**Example:**
```
"You're working on production code that serves millions of users. Prioritize reliability and maintainability over clever solutions."
```

---

## Common Patterns Summary

### For Coding Tasks:
```
1. Read relevant files FIRST
2. Understand existing patterns
3. Implement general solutions
4. Create tests
5. Verify correctness
6. Clean up temporary files
```

### For Analysis Tasks:
```
1. Understand the question
2. Gather relevant information
3. Think step-by-step
4. Consider alternatives (develop competing hypotheses)
5. Provide structured output
6. State confidence level
```

### For Creative Tasks:
```
1. Understand requirements
2. Avoid generic patterns
3. Request specific features explicitly
4. Use modifiers (comprehensive, creative, etc.)
5. Specify exact output format
```

### For Multi-Step Tasks:
```
1. Create a plan first
2. Break into sub-tasks
3. Execute incrementally
4. Track progress
5. Verify each step
6. Save state between turns
```

---

## Quick Reference Checklist

**Before sending any prompt, verify:**

- [ ] Critical instructions at the beginning
- [ ] Clear, direct language (MUST, NEVER, ALWAYS)
- [ ] Output format specified explicitly
- [ ] Context/reasoning provided for key rules
- [ ] Examples align with desired behavior (or Zero-Shot for reasoning models)
- [ ] Complex tasks broken into steps
- [ ] Reasoning depth matches task complexity
- [ ] Role/persona defined if needed
- [ ] Language specified (for multilingual models)
- [ ] Verification requirements included

**For Reasoning Models (o1, DeepSeek-R1, QwQ) also check:**
- [ ] Using zero-shot (not few-shot) - *Few-shot degrades performance*
- [ ] Reasoning/answer structure defined (e.g., `<think>` tags)
- [ ] Readability requirements specified (Summary at end)
- [ ] Language consistency enforced (Prevent mixing in reasoning blocks)
- [ ] Avoid "think" keyword if extended thinking is disabled (Claude specific)

---

## Final Tips

1.  **Be explicit over implicit** - Don't assume the model knows what you want.
2.  **Show, don't just tell** - Examples are powerful (unless using Reasoning models).
3.  **Test and iterate** - First prompts rarely work perfectly.
4.  **Longer is often better** - A detailed 500-word prompt beats a vague 50-word one.
5.  **Structure matters** - Use headings, sections, and clear formatting.
6.  **Context is key** - Explain the "why" behind your requirements.
7.  **Match Style** - If you want prose, write a prose prompt. If you want code, write a code-like prompt.

---

*This guide consolidates best practices from Claude 4.x, GLM-4.7, DeepSeek-R1, and other frontier models. Use it as a reference when crafting prompts for any LLM.*
```
