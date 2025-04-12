# LLM Lessons Learned Prompt

## Part 1: Metadata Suggestion & Confirmation Request

1. Analyse the preceding conversation thoroughly.  
2. Use today's date in the format `YYYY-MM-DD` (e.g., 2025-04-12).
3. Determine the primary **Topic**.  
   - Format: lowercase, hyphenated (e.g., `python-cachetools`, `email-spoofing-detection`)  
   - Be specific—if a particular technology, library, or method is central, reflect that in the topic.
4. Determine the most appropriate **Category**.  
   - Format: lowercase, hyphenated.  
   - Choose from: `programming`, `ai-interaction`, `data-analysis`, `writing`, `research`, `cyber-security`, `database`, `project-management`  
   - If none fit well, suggest a more suitable one.
5. Present the metadata suggestions clearly in the format below.
6. **Important:** Ask me to confirm or correct these values. **Do not generate the summary or filename yet.**

---

**Metadata Suggestions (Part 1):**

- **Suggested Date:** 2025-04-12  
- **Suggested Topic:** [LLM-suggested topic]  
- **Suggested Category:** [LLM-suggested category]  

**Please respond with:**
- **"Confirmed"** if these are correct
- **"Revise topic: [your topic]"** to change the topic
- **"Revise category: [your category]"** to change the category
- **"Revise both: [topic] / [category]"** to change both

---

## Part 2: Summary and Artefact Generation (Triggered by User Confirmation)

Once I confirm the values from Part 1:

- **Confirmed Date:** [confirmed]  
- **Confirmed Topic:** [confirmed]  
- **Confirmed Category:** [confirmed]

1. **Generate Filename Summary:**  
   Create a concise 4–5 word summary of the key lesson learned (lowercase, hyphenated).

2. **Construct Filename:**  
   Format: `[confirmed_category]-[confirmed_topic]-[filename-summary]-[confirmed_date].md`

3. **Create a Markdown Artefact:**  
   Generate a single well-structured Markdown document using the filename format above. Present it as an artifact (Claude), in canvas (ChatGpt/Gemini)

```markdown
# Lessons Learned: [Title Case Topic]

**Date:** [Confirmed Date]  
**Category:** [Confirmed Category]  
**Topic:** [Confirmed Topic]  
**Tags/Keywords:** [keyword1], [keyword2], [keyword3]

## Conversation Context & Goal
*Briefly summarise the goal or problem discussed (1–3 sentences).*

## Key Lessons Learned
* **Lesson 1:** [Key takeaway]  
* **Lesson 2:** [Optional second takeaway]  
* *(Add more if needed)*

## Supporting Details / Examples
* `Code snippets, prompt samples, or configs if relevant`  
* > Notable quote or insight from the conversation

## Pitfalls / Things to Avoid
* *(Optional: Ineffective approaches or known issues)*

## Related Concepts / Next Steps
* *(Optional: Further reading, follow-up ideas, or related work)*

## Reusable Best Practices
* **Practice 1:** [Broader principle that could be applied to other projects in this category]
* **Practice 2:** [Another transferable approach or method]
* *(Focus on abstract principles that transcend this specific implementation)*

## Glossary
* **Term 1:** Brief definition of technical term or concept from this lesson
* **Term 2:** Brief definition of another term
* *(Include only for topics with specialized terminology)*
```
