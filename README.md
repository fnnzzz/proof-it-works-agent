# 🔍 Proof It Works

An AI agent that replaces manual feature verification — opens a real browser, walks through your staging environment step by step, and hands you a pass/fail report. No QA engineer pulled away. No screen recording. No back-and-forth.

---

## 😤 The Problem We're Solving

Every sprint ends with the same bottleneck: _someone has to manually verify the feature works._

A developer finishes a task and wants to show it's working before handoff. QA needs a quick sanity check before formal execution. A product owner wants to see the feature live before a demo — but pulling a QA engineer for every pre-demo check is expensive and slow.

This is a fully manual, repetitive process. And it happens every sprint, on every task, across every team.

There's also a subtler cost hiding in every sprint — the dev ↔ QA loop:

> 👨‍💻 PR submitted → 🚀 deployed to staging → 🧪 QA goes in → ❌ missing button → 🔄 ticket returned → 👨‍💻 fix → 🚀 redeploy → 🧪 QA again → ...

Each cycle costs hours. And it's often something small that could've been caught in 2 minutes.

**Proof It Works** acts as a pre-validation layer — catching the obvious misses before the ticket ever reaches QA. Fewer round-trips, faster feature delivery. 🏓

You give it a task, it opens Chrome, navigates the staging app, runs the test cases, and hands you a report with screenshots — fully autonomously.

This is what we mean by less manual work, done by AI. 🤖

---

## 📈 Business Impact

| Before | After |
| --- | --- |
| QA engineer spends 20–40 min per manual check | Agent runs in the background while the team keeps working |
| Feature demo prep blocks QA capacity | PO runs pre-demo verification independently |
| Verification results live in someone's head or a Slack message | Structured markdown report saved automatically with screenshots |
| Hard to scale as the team grows | Agent handles more verifications as you ship more — no extra headcount |

**What scales:** as the team ships more features, the agent takes on more verification work — without slowing down delivery cycles. 🚀

---

## 👥 Who It's For

| Role | When to use it |
| --- | --- |
| 👨‍💻 **Developer** | See your task working end-to-end before it leaves your hands |
| 🧪 **QA** | Quick visual sanity check before formal test execution |
| 📋 **Product Owner** | Verify a feature on staging before an internal demo or stakeholder review |
| 🤝 **PO + QA together** | Run a pre-demo session autonomously, without blocking the QA team |

---

## ⚙️ How It Works

1. 📎 **You give it a task** — paste an Azure DevOps URL/ID, or just describe what to test in plain text
2. 📥 **It fetches the details** — if you pass an Azure DevOps task, it automatically pulls the title, description, acceptance criteria, and all AQA test cases linked to it; otherwise you describe what to test yourself
3. ❓ **It asks a few quick questions** in one message — login needed? any API mocks? edge cases to add?
4. 🌐 **It opens Chrome via Playwright** and navigates to the staging environment
5. 🖱️ **It runs each test case**, highlighting every element it interacts with so you can follow along visually
6. 🔔 **After each test case**, it reports pass ✅ or fail ❌ immediately
7. 📄 **At the end**, it saves a full report with screenshots to `.claude/agents/proof-it-works/artifacts/`

Everything happens in a real browser — you see exactly what the agent sees.

---

## 🚀 How to Use It

### Setup

```bash
git clone https://github.com/fnnzzz/proof-it-works-agent.git
cd proof-it-works-agent
claude
```

No install. No config. Three commands and you're running.

---

### Option A — Azure DevOps task ✨ _(recommended)_

Paste a task URL or ID:

```
proof it works 111861
```

```
proof it works https://dev.azure.com/org/project/_workitems/edit/111861
```

The agent pulls the title, description, acceptance criteria, and all AQA test cases linked to the task — automatically, with no manual setup. Just paste the link and go.

> The Azure DevOps MCP connection is already configured in the repo — nothing to set up. See the [Azure DevOps Integration](#-azure-devops-integration) section below if you're curious how it works.

---

### Option B — Free text 💬 _(works anywhere, zero dependencies)_

No integrations, no prerequisites. Just describe what you want to test:

```
proof it works — check that the BTC/USD chart loads correctly on the asset page and the WEEK timeframe switch works
```

Works without any external connections. You describe the feature, the agent builds the test cases and runs them.

---

### 🎯 Choosing which test cases to run

After the agent builds the test plan, you can tell it exactly what to run:

- **All of them** — say `"looks good"` and it runs everything
- **Specific ones** — `"run only TC-74123 and TC-74125"`
- **Your own** — describe additional cases and the agent adds them before starting

You can also mix: run the AQA-linked test cases plus a few extra edge cases you describe yourself.

---

### 🔧 API mocks

When the agent asks about mocks, you can say things like:

- _"Pre-fill an open limit BUY order for BTC/USD at $30,000"_
- _"Make all DELETE requests return 200 OK"_
- _"Return a fixed balance of $10,000 on GET /accounts"_

The agent overrides `window.fetch` in the browser session so it looks like the data is coming from the backend — without touching any real data.

---

### 🔐 Login

If the feature requires auth, the agent navigates to the login page and waits for you to enter your credentials manually. It never stores or logs passwords.

---

## 🎁 What You Get

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

## 🔗 Azure DevOps Integration

### Is it required?

Nope. The Azure DevOps integration is an enhancement, not a dependency. If you'd rather just describe what to test in plain text, go with Option B — it works great on its own.

### What does it actually do?

When connected, the agent reads your task directly from Azure DevOps: the title, description, acceptance criteria, and any AQA test cases linked to the work item. This saves you from copying that info manually.

It's **read-only**. The agent never writes to Azure DevOps, creates tickets, modifies test cases, or changes anything. It only fetches task metadata to build its test plan. That's it.

### How does it connect — and is it safe? 🔒

The integration uses **MCP (Model Context Protocol)** — a standardized protocol for letting AI tools securely access external services. Think of it as a controlled bridge: the agent requests specific data, Azure DevOps responds, and nothing else happens.

Authentication happens through your own browser — it uses your existing Azure DevOps session, so no tokens, no credentials, nothing to configure.

### How to enable it

Already configured. When you start the agent, Claude will ask if you want to use Azure DevOps — just say yes. Nothing else needed.

---

## 📚 Examples

See the [`examples/`](./.claude/agents/proof-it-works/examples/) folder for ready-to-paste task descriptions covering common flows.
