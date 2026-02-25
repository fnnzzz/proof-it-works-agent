# 🔍 Proof It Works

A Claude agent that walks through your features on the staging environment — visually, step by step, exactly like a QA engineer would.

---

## 🛠️ Getting started

```bash
git clone https://github.com/fnnzzz/proof-it-works-agent.git
cd proof-it-works-agent
claude
```

That's it. No install, no config.

---

## 🤔 Why

Every sprint ends with the same question: _show me how it works._

Not just "does it work" — but walk me through it. Show me the flow, the edge cases, what happens when you click that button. Developers want to see their task working end-to-end before handing it off. QA testers want a quick visual pass before diving into deep test scenarios. Product owners want to see the feature live before a demo, without pulling someone from the QA team for every check.

**Proof It Works** handles all of that autonomously. You give it a task link (or just describe what you want to test), and it opens a real browser, navigates the staging app, runs through the test cases, highlights every element it touches, and gives you a clear pass/fail report at the end.

No code. No setup. Just results.

---

## 👥 Who it's for

| Role                    | When to use it                                                        |
| ----------------------- | --------------------------------------------------------------------- |
| 👨‍💻 **Developer**        | See your task working all together before it leaves your hands        |
| 🧪 **QA**               | Quick visual sanity check before formal test execution                |
| 📋 **Product Owner**    | Verify a feature on dev before an internal demo or stakeholder review |
| 🤝 **PO + QA together** | Run a pre-demo session autonomously, without blocking the QA team     |

---

## ⚙️ How it works

1. 📎 **You give it a task** — paste an Azure DevOps URL/ID, or just describe what to test in plain text
2. 📥 **It fetches the details** — task description, acceptance criteria, and **all test cases written by AQA and linked to the task are pulled automatically**
3. ❓ **It asks a few quick questions** in one message — login needed? any API mocks? edge cases to add?
4. 🌐 **It opens Chrome via Playwright** and navigates to the staging environment
5. 🖱️ **It runs each test case**, highlighting every element it interacts with so you can follow along visually
6. 🔔 **After each test case**, it reports pass ✅ or fail ❌ immediately
7. 📄 **At the end**, it saves a full report with screenshots to `.claude/agents/proof-it-works/artifacts/`

Everything happens in a real browser — you see exactly what the agent sees.

---

## 🚀 Usage

### Option A — Azure DevOps task ✨ recommended

Paste a task URL or ID:

```
proof it works 111861
```

```
proof it works https://dev.azure.com/org/project/_workitems/edit/111861
```

The magic: the agent pulls the title, description, acceptance criteria, and **all AQA test cases linked to the task — automatically, with no manual setup**. Just paste the link and go.

> **⚠️ Azure DevOps MCP required.** This option needs the Azure DevOps MCP server connected in your Claude Code environment. If it's not available, use Option B below.

### Option B — Free text

No integrations, no prerequisites. Just describe what you want to test:

```
proof it works — check that the BTC/USD chart loads correctly on the asset page and the WEEK timeframe switch works
```

Works anywhere, zero dependencies. You describe the feature, the agent figures out the test cases and runs them.

### 🎯 Choosing which test cases to run

After the agent builds the test plan, you can tell it exactly what to run:

- **All of them** — say `"looks good"` and it runs everything
- **Specific ones** — `"run only TC-74123 and TC-74125"`
- **Your own** — describe additional cases and the agent adds them to the plan before starting

You can also mix: **run the AQA-linked test cases plus a few extra edge cases you describe yourself.**

### 🔧 API mocks

When the agent asks about mocks, you can say things like:

- _"Pre-fill an open limit BUY order for BTC/USD at $30,000"_
- _"Make all DELETE requests return 200 OK"_
- _"Return a fixed balance of $10,000 on GET /accounts"_

The agent overrides `window.fetch` in the browser session so it looks like the data is coming from the backend — without touching any real data.

### 🔐 Login

If the feature requires auth, the agent navigates to the login page and waits for you to enter your credentials manually. It never stores or logs passwords.

---

## 🎁 What you get

- 🟠 **Live visual feedback** — focused elements are highlighted in orange as the agent interacts with them
- 🔔 **Per-test-case results** printed immediately after each one runs
- 📄 **A full markdown report** saved to the artifacts folder with pass/fail status, screenshots, and bug notes for any failures
- 📸 **Screenshots** of every meaningful state change

---

## 📁 Artifacts

```
.claude/agents/proof-it-works/artifacts/
  {task-id}-{slug}/
    report.md
    screenshots/
      TC74123-step1-...png
      TC74123-step2-...png
      ...
```

If you run the same task again, a timestamp suffix is added so previous results are never overwritten.

---

## 📚 Examples

See the [`examples/`](./examples/) folder for ready-to-paste task descriptions covering common flows.
