## Prompt: Convert Microsoft Forms JSON to Structured Markdown

### 🔧 Purpose
Transform raw Microsoft Forms JSON data into a well-structured markdown document that replicates the original form layout. This includes all questions, section headers, choice options, and required field indicators.

---

### 🤔 Background
Microsoft Forms JSON (retrieved via browser dev tools or internal APIs) contains both questions and section metadata:

- `questions[]` = the actual survey questions
- `descriptiveQuestions[]` = section labels, often represented by `Question.ColumnGroup`
- `order` = float indicating display order
- `title` or `formsProRTQuestionTitle` = the actual question text
- `questionInfo` (JSON-encoded string) = detailed metadata
  - `Choices[]`: options for multiple choice questions
  - `ChoiceType`: 0 = text, 1 = single choice, 2 = multi choice
  - `AllowOtherAnswer`: true if "Other" option is allowed
  - `Multiline`: true if long text field
  - `Length` and `RatingShape`: for star/number ratings
  - `Date` and `Time`: for datetime pickers
  - `FileTypes`, `MaxFileSize`, etc.: for file upload questions
- `type` may include (examples):
  - `Question.TextField`
  - `Question.Choice`
  - `Question.Rating`
  - `Question.DateTime`
  - `Question.Ranking`
  - `Question.MatrixChoiceGroup` and `Question.MatrixChoice`
  - `Question.FileUpload`
  - `Question.NPS`

---

### 🔀 What to Generate
Generate a markdown document with:

- Section headers (from `descriptiveQuestions`, sorted by `order`)
- Numbered questions under each section (from `questions`, sorted by `order`)
- Indicate required questions
- List choice options where present
- Mark question type if not obvious (e.g. text, date, rating)
- Indicate grouped questions (e.g. matrix Likert blocks)
- Show expected file types or max file size for file uploads

---

### ✉️ Example Input (Anonymised)
```json
{
  "title": "Cat Survey Deluxe",
  "descriptiveQuestions": [
    {"title": "General Info", "order": 1000, "type": "Question.ColumnGroup"},
    {"title": "Feeding Habits", "order": 2000, "type": "Question.ColumnGroup"}
  ],
  "questions": [
    {"title": "What's your cat's name?", "order": 1100, "required": true, "type": "Question.TextField"},
    {"title": "Cat's birthdate", "order": 1200, "required": true, "type": "Question.DateTime", "questionInfo": "{\"Date\":true}"},
    {"title": "Preferred food type?", "order": 2100, "required": true, "type": "Question.Choice", "questionInfo": "{\"Choices\":[{\"Description\":\"Dry\"},{\"Description\":\"Wet\"}],\"ChoiceType\":1}"},
    {"title": "How many meals daily?", "order": 2200, "type": "Question.Rating", "questionInfo": "{\"RatingShape\":\"Number\",\"Length\":5}"},
    {"title": "Upload a picture", "order": 2300, "type": "Question.FileUpload", "required": false, "questionInfo": "{\"MaxFileSize\":10,\"FileTypes\":{\"Image\":true}}"}
  ]
}
```

---

### 🗾️ Example Output (Markdown)
```markdown
## Cat Survey Deluxe (Markdown Version)

### Section 1: General Info

1. **What's your cat's name?**  
*Required*  
_Type: Short text_

2. **Cat's birthdate**  
*Required*  
_Type: Date picker_

---

### Section 2: Feeding Habits

3. **Preferred food type?**  
*Required, single choice*  
- Dry  
- Wet

4. **How many meals daily?**  
_Type: Number rating (1–5)_

5. **Upload a picture**  
_Optional_  
_Type: File upload (Max 10MB, Images only)_
```

---

### 💭 Additional Tips
- Use `formsProRTQuestionTitle` if `title` is missing or contains HTML
- Group Likert items (`Question.MatrixChoice`) under their `Question.MatrixChoiceGroup` parent
- Sort both `questions` and `descriptiveQuestions` by `order`
- Display file restrictions clearly (e.g. file type, max size)
- Treat rating stars/numbers distinctly using `RatingShape`

---
