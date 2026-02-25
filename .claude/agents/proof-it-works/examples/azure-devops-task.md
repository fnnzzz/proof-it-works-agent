# Example: Azure DevOps Task by ID or URL

Paste either of these to the agent — it will fetch the task automatically:

---

**By numeric ID:**
```
111861
```

**By full URL:**
```
https://dev.azure.com/FinoCRM/XBO/_workitems/edit/111861
```

---

The agent will:
- Fetch the task title, description, and acceptance criteria from Azure DevOps
- Pull all linked test cases (added by Automation QA under "Tested By")
- Show you a short summary, then ask about login, mocks, and any extra edge cases you want covered

This is the recommended approach when the task already has test cases linked — the agent builds the test plan from them automatically.
