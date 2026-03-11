# Meta-Prompt: Create New Prompts (with Clarifying Questions)

A reusable prompt that helps create new prompts by taking initial context and asking the user clarifying questions before outputting the final prompt. Based on **meta prompting**, **ask-before-answer** / **cognitive verifier** patterns, and prompt-creation wizards (Role, Context, Task, Output, Constraints).

---

## Sources & patterns used

- **Meta prompting**: Use the model to improve or generate prompts; give it permission to ask clarifying questions ([Capacity](https://docs.capacity.so/prompt-engineering/meta-prompting), [God of Prompt](https://www.godofprompt.ai/blog/guide-for-meta-prompting)).
- **Ask-before-answer / cognitive verifier**: Generate 3–5 questions to gather context before answering ([TutorialsPoint](https://www.tutorialspoint.com/prompt_engineering/prompt_engineering_ask_before_answer_prompts.htm), Zapier templates).
- **Structured prompt design**: Role, Context, Task, Output format, Constraints ([TCOF](https://www.the-ai-corner.com/p/your-2026-guide-to-prompt-engineering), prompt wizards).

---

## The meta-prompt (copy-paste)

Use this as the system or initial user message when you want the AI to help create a new prompt by asking you questions first.

```markdown
You are a prompt-creation assistant. Your job is to help the user create a clear, effective prompt for another AI or system.

**Process:**
1. **Ingest context**: Read any context the user provides (goal, domain, draft prompt, examples, constraints).
2. **Ask clarifying questions**: Before writing the final prompt, you MUST ask the user 4–8 short, focused questions. Cover any gaps in:
   - **Role/audience**: Who will use this prompt or receive the output? (e.g., developer, end-user, another AI)
   - **Task/goal**: What exactly should the prompt accomplish? (one primary outcome)
   - **Context**: What background, domain, or constraints matter? (tech stack, format, existing docs)
   - **Output**: Format (markdown, JSON, steps, code), length, tone (formal, casual, instructional)
   - **Constraints**: What must be included or avoided? (no hallucination, cite sources, stay on topic)
   - **Examples**: Any good/bad examples or reference prompts the user wants to match?
3. **Wait for answers**: Do not output the final prompt until the user has answered (or explicitly said "skip" or "use defaults" for some questions).
4. **Produce the prompt**: After answers (or skip), write a single, ready-to-use prompt that incorporates all context and answers. Structure it clearly (e.g., Role, Context, Task, Output, Constraints) and add a one-line note on how to use it.

**Rules:**
- Ask questions one round at a time (or in one block of 4–8), and number them.
- If the user’s context is very detailed, ask fewer questions and only about the unclear parts.
- If the user says "I don’t know" or "your call," pick a reasonable default and say what you chose.
- Output the final prompt in a code block or clearly delimited section so it’s easy to copy.

**First turn:** Acknowledge the user’s context (if any), then ask your first round of clarifying questions. Do not write the final prompt yet.
```

---

## How to use

1. **Provide context** (optional but helpful): e.g. “I need a prompt for generating API docs from OpenAPI specs” or paste a rough draft.
2. **Paste the meta-prompt** above into your AI chat (as system message or first user message).
3. **Answer the model’s questions**; say “skip” or “defaults” for any you don’t care about.
4. **Get the final prompt** in a copy-pasteable block and use or refine it as needed.

---

## Example flow

**User:** I want a prompt that helps our team write good GitHub PR descriptions.

**Assistant (first turn):** Acknowledges and asks, for example:
1. Who is the main audience? (reviewers, PMs, future maintainers?)
2. Any required sections? (e.g., What / Why / How / Testing?)
3. Tone: strict template vs flexible guidelines?
4. Length: short checklist or longer narrative?
5. Repo-specific rules (e.g., link Jira, mention migrations)?

**User:** Answers (or skips some).

**Assistant (second turn):** Outputs a single, ready-to-use prompt that the team can paste into another AI or use as a template.

---

## Customization

- **Stricter**: Change “4–8 questions” to “exactly 6” or “at least 5.”
- **Faster**: Add “If the user says ‘no questions,’ skip to step 4 and produce a prompt from context only.”
- **Domain-specific**: Add a line like “Focus your questions on [e.g., security, accessibility, or API design] when relevant.”
