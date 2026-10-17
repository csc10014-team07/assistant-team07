# AI Service: 10 Questions That Need AI vs 10 That Do Not

This document defines the boundary between deterministic (rule-based / database lookup) queries and queries that require an AI service (LLM / Natural Language Understanding) for the campus assistant.

## Summary & Classification Criteria

- **Does NOT need AI (Deterministic)**: Factual queries resolvable via structured table lookups (e.g. `offices.csv`), static text responses (greetings, help text, system status), exact string matching, or straightforward rule validation.
- **Needs AI (LLM / Semantic reasoning)**: Unstructured inquiries requiring semantic parsing, intent extraction, multi-condition reasoning, paraphrasing/slang comprehension, multi-turn context resolution, policy document synthesis, or open-ended advice.

---

## 1. Ten Questions That Do NOT Need AI

| # | Question | Query Type | Needs AI | One-line Reason |
| :-: | :--- | :--- | :-: | :--- |
| 1 | "Where is the Training Office?" | Exact location lookup | **No** | Can be resolved by direct string matching against `name` in `data/offices.csv`. |
| 2 | "When does the library open?" | Exact hours lookup | **No** | Deterministic lookup from the structured `hours` column in `data/offices.csv`. |
| 3 | "Hello" / "Xin chào" | Greeting | **No** | Handled by a static keyword dictionary without semantic interpretation. |
| 4 | "help" | Help command | **No** | Fixed text output listing bot capabilities and usage instructions. |
| 5 | "List all campus offices" | Data dump | **No** | Simple select query returning all office names directly from `data/offices.csv`. |
| 6 | "What office is in room I.101?" | Reverse lookup | **No** | Deterministic key lookup mapping room identifier back to office record. |
| 7 | "What is the security emergency phone number?" | Fixed contact | **No** | Static contact retrieval from hardcoded configuration or key-value store. |
| 8 | `""` (empty message or whitespace) | Input validation | **No** | Trivial string emptiness check handled in code via `message.strip()`. |
| 9 | "IT Helpdesk room and hours" | Multi-attribute lookup | **No** | Simple regex/keyword match retrieving the complete row for `IT Helpdesk`. |
| 10 | "What version is this assistant?" | System metadata | **No** | Deterministic metadata retrieval from package configuration (`pyproject.toml`). |

---

## 2. Ten Questions That DO Need AI

| # | Question | Query Type | Needs AI | One-line Reason |
| :-: | :--- | :--- | :-: | :--- |
| 1 | "Chỗ nào để tôi rút học bạ và làm thủ tục bảo lưu vậy bot?" | Intent & office mapping | **Yes** | Requires semantic parsing to identify student intent and map to appropriate offices. |
| 2 | "Tôi muốn xin bảng điểm gấp vào sáng thứ Bảy thì có văn phòng nào mở không?" | Multi-constraint reasoning | **Yes** | Requires reasoning across multiple office schedules and transcript issuance procedures. |
| 3 | "Điều kiện để được xét học bổng khuyến khích học tập kỳ này là gì?" | Policy document synthesis | **Yes** | Requires extracting, interpreting, and summarizing criteria from university regulation texts. |
| 4 | "Văn phòng đó có làm việc vào buổi chiều không?" | Coreference resolution | **Yes** | Requires conversational memory to resolve what "văn phòng đó" refers to from prior context. |
| 5 | "Em năm nhất ngành CNTT nên đăng ký môn tiên quyết nào trước?" | Academic advising | **Yes** | Requires analyzing curriculum prerequisite graphs and generating personalized guidance. |
| 6 | "Pls chi minh cho nop don xin mien giam hoc phi voi a?" | Noisy & informal text | **Yes** | Requires natural language normalization to handle abbreviations, typos, and student slang. |
| 7 | "Em bị trượt môn Giải tích cảm thấy rất nản, em nên làm gì bây giờ?" | Empathetic guidance | **Yes** | Requires sentiment comprehension and empathetic tone synthesis combined with academic recovery steps. |
| 8 | "Nếu lịch thi của em bị trùng 2 môn cùng ca thì phải xử lý thế nào?" | Procedural problem-solving | **Yes** | Requires multi-step procedural reasoning based on examination rules and petition workflows. |
| 9 | "Tóm tắt thông báo đăng ký học phần đợt 2 cho sinh viên khóa 2023" | Document summarization | **Yes** | Requires summarizing long-form official announcement text into concise deadlines and action items. |
| 10 | "Sinh viên mới nên tham gia CLB nào để rèn luyện kỹ năng lập trình?" | Tailored recommendation | **Yes** | Requires understanding student profile and synthesizing qualitative club recommendations. |

---

## 3. Master Comparison Table

| # | Question | Needs AI | One-line Reason |
| :-: | :--- | :-: | :--- |
| 1 | "Where is the Training Office?" | **No** | Can be resolved by direct string matching against `name` in `data/offices.csv`. |
| 2 | "When does the library open?" | **No** | Deterministic lookup from the structured `hours` column in `data/offices.csv`. |
| 3 | "Hello" / "Xin chào" | **No** | Handled by a static keyword dictionary without semantic interpretation. |
| 4 | "help" | **No** | Fixed text output listing bot capabilities and usage instructions. |
| 5 | "List all campus offices" | **No** | Simple select query returning all office names directly from `data/offices.csv`. |
| 6 | "What office is in room I.101?" | **No** | Deterministic key lookup mapping room identifier back to office record. |
| 7 | "What is the security emergency phone number?" | **No** | Static contact retrieval from hardcoded configuration or key-value store. |
| 8 | `""` (empty message or whitespace) | **No** | Trivial string emptiness check handled in code via `message.strip()`. |
| 9 | "IT Helpdesk room and hours" | **No** | Simple regex/keyword match retrieving the complete row for `IT Helpdesk`. |
| 10 | "What version is this assistant?" | **No** | Deterministic metadata retrieval from package configuration (`pyproject.toml`). |
| 11 | "Chỗ nào để tôi rút học bạ và làm thủ tục bảo lưu vậy bot?" | **Yes** | Requires semantic parsing to identify student intent and map to appropriate offices. |
| 12 | "Tôi muốn xin bảng điểm gấp vào sáng thứ Bảy thì có văn phòng nào mở không?" | **Yes** | Requires reasoning across multiple office schedules and transcript issuance procedures. |
| 13 | "Điều kiện để được xét học bổng khuyến khích học tập kỳ này là gì?" | **Yes** | Requires extracting, interpreting, and summarizing criteria from university regulation texts. |
| 14 | "Văn phòng đó có làm việc vào buổi chiều không?" | **Yes** | Requires conversational memory to resolve what "văn phòng đó" refers to from prior context. |
| 15 | "Em năm nhất ngành CNTT nên đăng ký môn tiên quyết nào trước?" | **Yes** | Requires analyzing curriculum prerequisite graphs and generating personalized guidance. |
| 16 | "Pls chi minh cho nop don xin mien giam hoc phi voi a?" | **Yes** | Requires natural language normalization to handle abbreviations, typos, and student slang. |
| 17 | "Em bị trượt môn Giải tích cảm thấy rất nản, em nên làm gì bây giờ?" | **Yes** | Requires sentiment comprehension and empathetic tone synthesis combined with academic recovery steps. |
| 18 | "Nếu lịch thi của em bị trùng 2 môn cùng ca thì phải xử lý thế nào?" | **Yes** | Requires multi-step procedural reasoning based on examination rules and petition workflows. |
| 19 | "Tóm tắt thông báo đăng ký học phần đợt 2 cho sinh viên khóa 2023" | **Yes** | Requires summarizing long-form official announcement text into concise deadlines and action items. |
| 20 | "Sinh viên mới nên tham gia CLB nào để rèn luyện kỹ năng lập trình?" | **Yes** | Requires understanding student profile and synthesizing qualitative club recommendations. |

---

## 4. Recommended Architectural Routing Logic

```text
User Question
    │
    ├── [Is Empty / Whitespace?] ───> Return "Please type a question." (Deterministic)
    │
    ├── [Matches Static Greetings/Commands?] ───> Return Predefined Response (Rule-based)
    │
    ├── [Matches Office / Room in CSV?] ───> Return Row Record from CSV (Lookup)
    │
    └── [Complex / Semantic / Unmatched] ───> Forward to AI Service (LLM / RAG)
```
