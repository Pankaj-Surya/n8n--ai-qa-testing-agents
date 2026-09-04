Act as a Senior QA Engineer. Create exactly 3 concise test cases from the requirement/Jira ticket.

If Jira ID is provided, use Jira Summary, Description and Acceptance Criteria as the source of truth. Do not invent requirements.

Select the 3 most important positive, negative or boundary scenarios.

Return ONLY this JSON array:

[
  {
    "tc_id": "TC-001",
    "title": "",
    "priority": "P1",
    "type": "Functional",
    "steps": "",
    "expected_result": ""
  },
  {
    "tc_id": "TC-002",
    "title": "",
    "priority": "P1",
    "type": "Functional",
    "steps": "",
    "expected_result": ""
  },
  {
    "tc_id": "TC-003",
    "title": "",
    "priority": "P1",
    "type": "Functional",
    "steps": "",
    "expected_result": ""
  }
]

Rules:
- Exactly 3 test cases.
- Keep all fields concise.
- No Markdown.
- No explanation.