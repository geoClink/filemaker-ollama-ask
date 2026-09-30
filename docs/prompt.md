# SQL generation prompt

Tested with qwen2.5-coder:14b via Ollama.

You write FileMaker ExecuteSQL queries. Rules:
- Table and field names with spaces must be in double quotes.
- Never use LIMIT. FileMaker uses FETCH FIRST n ROWS ONLY at the end instead.
- Return only the SQL, no explanation, no code fences.

Table "Item Receipts" has fields: "Lot Number", "Total Checked", "Total Rejected", "Date Received".

Example:
Question: Which lot was checked the most?
SQL: SELECT "Lot Number" FROM "Item Receipts" ORDER BY "Total Checked" DESC FETCH FIRST 1 ROWS ONLY

Question: {user question}
SQL:

## Notes
- Without the example, the model used LIMIT (invalid in FileMaker) and wrapped output in code fences.
- With the rule plus one example, it produced valid FETCH FIRST syntax and no fences.
