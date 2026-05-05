# Government of British Columbia — GitHub Copilot Train-the-Trainer

**Date:** May 5, 2026
**Cohort:** Government of British Columbia
**Format:** Train-the-Trainer (demo + hands-on + enablement)
**Primary lab:** [`asset-manager/`](../asset-manager) — Spring Boot Java app → Azure

## Facilitators

- **Ve Sharma** — Solution Engineer, Dev Tools & GitHub, Microsoft
- **Venkat Gowrishankar** — Sr. Cloud & AI Specialist, Microsoft

---

## 🧭 Objectives

By the end of this session, participants will:

1. Understand **GitHub Copilot as an agentic development capability** (not just autocomplete).
2. Use **Copilot CLI and Copilot Chat** for real-world engineering tasks.
3. Apply Copilot to **modernize a Java application** end-to-end.
4. Learn how to **teach Copilot internally** within their teams.
5. Understand **agentic governance** and public-sector considerations.
6. Take away a concrete plan to **internally enable BC Gov developers**.

---

## 🗂️ Agenda

| # | Section | Time |
|---|---------|------|
| 1 | Welcome + Context | 15 min |
| 2 | GitHub Copilot: What's New | 15 min |
| 3 | Copilot CLI + Agent Workflows | 30 min |
| 4 | Agentic Governance & Policy Controls | 20 min |
| 5 | **Java App Modernization Lab** ([`asset-manager/`](../asset-manager)) | 1.5 hr |
| 6 | Train-the-Trainer Model | 45 min |
| 7 | Governance + Public-Sector Considerations | 15 min |

---

## 1️⃣ Welcome + Context (15 min)

- Why this matters for the **Government of British Columbia**.
- Copilot as a **developer capability**, not just a tool.
- Set expectations: **demo vs. hands-on vs. teaching**.

---

## 2️⃣ GitHub Copilot: What's New (15 min)

- Copilot across **IDE, GitHub.com, and CLI**.
- Shift from suggestions to **agentic workflows**.
- The agent loop: **Plan → Act → Validate**.

✅ Quick demo prompt:

> *"Analyze this repo and propose a modernization plan before making any changes."*

---

## 3️⃣ Copilot CLI + Agent Workflows (30 min)

### Key concepts

- **Context engineering** — supplying architecture, policies, and docs to the agent.
- **Multi-agent scenarios** — separating app work from infra work from validation.
- **Human-in-the-loop control** — when to require approval.

### ✅ Hands-on

Participants will:

1. Analyze a repository with Copilot CLI / Chat.
2. Generate a modernization plan.
3. Refine outputs with iterative prompts.

---

## 4️⃣ Agentic Governance & Policy Controls (20 min)

### 🎯 Objective

Enable teams to use GitHub Copilot as a **secure, governed capability at scale**.

### 🔐 Why governance matters (BC Gov context)

Copilot introduces AI into the **SDLC decision process**. It must align with:

- Data handling policies
- Security and compliance standards

✅ **Treat Copilot like a production dependency — governed, not optional.**

### 🧩 Core governance controls

**1. Model controls**
- Control **which AI models** are allowed.
- Restrict **where they can be used** (IDE, GitHub.com, CLI).
- 👉 Ensures approved, compliant AI usage.

**2. MCP server controls**
- Define which **tools/systems** agents can access.
- Restrict external endpoints and sensitive data access.
- 👉 Prevents data leakage and uncontrolled actions.

**3. GitHub + Copilot admin controls**
- Enable/disable Copilot by org/team/repo.
- Apply policies (suggestions, public-code filtering).
- Track usage and audit activity.
- 👉 Provides central governance and visibility.

**4. APM — Agent Package Manager (CRITICAL)**

👉 Repo: <https://github.com/microsoft/apm>

APM is the open-source dependency manager for AI agents — think `package.json`,
`requirements.txt`, or `Cargo.toml`, but for agent configuration (instructions,
skills, prompts, MCP servers). It is **portable by manifest, secure by default, and
governed by policy.**

What it does:

- Declares every primitive an agent needs (instructions, skills, prompts, MCP
  servers) in a single `apm.yml`, then `apm install` reproduces the exact same setup
  across Copilot, Claude, Cursor, and other clients.
- Lets a security team publish an `apm-policy.yml` that says *"these are the only
  sources, scopes, and primitives this org will allow"* — every `apm install`
  enforces it, with tighten-only inheritance from enterprise → org → repo.
- Scans for hidden Unicode / prompt-injection in packages before agents read them
  (`apm install` and `apm audit`).
- Pins integrity hashes in `apm.lock.yaml` for full provenance.
- Gates transitive MCP servers behind explicit trust prompts.

✅ Why APM matters for BC Gov:

- **Control actions** → block unsafe or unsanctioned packages before they reach an agent.
- **Enforce policy** → embed security and compliance into every developer's setup.
- **Reproducibility** → every developer who clones a repo gets the same configured agent.
- **Audit & provenance** → lockfile + hashes give you a defensible record.
- 👉 Especially critical for **public sector + multi-team rollout**.

### ⚖️ Key takeaway

> Without governance → Copilot is **helpful**.
> With governance (admin controls **+** APM **+** model/MCP controls) → Copilot is
> **trusted and scalable**. APM **complements** the GitHub and Copilot admin controls
> above; it does not replace them — together they form the full governance picture.

---

## 5️⃣ Java App Modernization Lab (1.5 hr)

**Repo:** <https://github.com/VeVarunSharma/java-app-modernization-workshop>
**Lab:** [`asset-manager/`](../asset-manager) — full guide and screenshots in
[`asset-manager/README.md`](../asset-manager/README.md).

### 🎯 Objective

Modernize a real Java application using GitHub Copilot (Chat + CLI + agent workflows) to:

- Assess modernization readiness
- Generate upgrade recommendations
- Apply changes with AI assistance
- Validate and prepare for cloud deployment

### 🧠 Workshop flow (phased learning)

#### Phase 1 — 🔎 Repo Exploration + Context Setup *(10–15 min)*

✅ **Goal:** build shared understanding + context for Copilot.

Participants will clone and open the repo, then review:

- `pom.xml` / `build.gradle`
- Dependency structure
- Java runtime version
- Application architecture

✅ **Prompt example:**

> *"Analyze this Java application and summarize its architecture, dependencies, and modernization opportunities. Identify risks and target state (Java version + cloud readiness)."*

#### Phase 2 — 📊 Modernization Assessment *(20 min)*

✅ **Goal:** generate a structured modernization plan.

Participants will use Copilot to identify:

- Outdated Java versions (e.g., Java 8 → 17+)
- Deprecated APIs
- Vulnerable or outdated dependencies
- Cloud readiness gaps

✅ **Prompt example:**

> *"Create a modernization plan to upgrade this application to Java 17+ and prepare it for deployment in a cloud-native environment."*

✅ **Expected outputs:**

- Modernization roadmap
- Risk analysis
- Dependency upgrade recommendations
- Target architecture (e.g., containerized / cloud-ready)

#### Phase 3 — ⚙️ Apply Modernization Changes *(30–40 min)*

✅ **Goal:** move from analysis → execution.

Participants will use Copilot to:

- Upgrade dependencies
- Refactor deprecated code
- Improve structure and maintainability
- Introduce modern configuration (env vars, external config)

✅ **Prompt pattern:**

> *"Apply the modernization steps incrementally. Show all changes, explain why they are needed, and validate after each step."*

✅ **Key learning:** Copilot is not just generating code — it is helping **execute and reason** through changes step-by-step.

#### Phase 4 — ✅ Validation + Testing *(15–20 min)*

✅ **Goal:** ensure the modernization works correctly.

Participants will build and run the application, then use Copilot to:

- Fix errors
- Update or add tests
- Identify regressions

✅ **Prompt example:**

> *"Validate this upgraded application and highlight runtime risks, missing dependencies, or potential failures in production."*

#### Phase 5 — ☁️ Cloud Readiness + Deployment *(optional stretch / discussion)*

✅ **Goal:** connect modernization → business value.

Discussion and/or demo:

- Containerization (Dockerfile generation)
- Deploying to cloud platforms (Azure Container Apps / AKS / OpenShift / App Service)
- Observability + monitoring considerations

✅ **Prompt example:**

> *"Generate a Dockerfile and deployment recommendations for this application to run in a cloud environment."*

✅ **Key takeaway:** modernization is not complete until the app is **deployable, observable, and scalable**.

---

## 6️⃣ Train-the-Trainer Model (45 min)

### 🎯 Objective

Enable participants to run this internally across **BC Gov teams**.

### 🧩 Internal enablement model

Recommended structure:

| Session | Format | Duration |
|---|---|---|
| **Session 1** | Awareness | 1 hr |
| **Session 2** | Hands-on workshop | half-day |
| **Session 3** | Team-specific deep dive | varies |

### 👥 Champion model

- 1–2 **Copilot Champions** per team.
- Run **office hours**.
- Share prompts and best practices.

### 📚 Prompt-sharing strategy

Use an internal repo or Teams/SharePoint hub, with reusable prompts for:

- Modernization
- Debugging
- Testing
- Documentation

### 📊 Measuring success

Track:

- Developer productivity improvements
- PR cycle time
- Code quality
- Backlog reduction

---

## 7️⃣ Governance + Public-Sector Considerations (15 min)

- Responsible Copilot usage.
- Data-handling considerations.
- Aligning with **BC Gov policies**.

✅ **Emphasize:**

- Treat Copilot as a **governed capability**.
- Apply the **same standards** as any developer tooling.

---

## ✅ Pre-workshop requirements

Participants **must** have the following installed and signed in:

- **GitHub account** with **GitHub Copilot** access (Pro, Pro+, Business, or Enterprise plan).
- **[Visual Studio Code](https://code.visualstudio.com/)** (1.101 or later) with the **GitHub Copilot** and **GitHub Copilot Chat** extensions.
- **[GitHub Copilot App Modernization for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.migrate-java-to-azure)** VS Code extension. *(In VS Code Settings, ensure `chat.extensionTools.enabled` is `true` — your org may control this.)*
- **[GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli)** — the standalone agentic CLI (`copilot`):
  ```bash
  # macOS / Linux
  curl -fsSL https://gh.io/copilot-install | bash      # or: brew install copilot-cli
  # Windows
  winget install GitHub.Copilot
  # cross-platform via npm
  npm install -g @github/copilot
  ```
  After install, run `copilot` and complete `/login`.
- **[Git CLI](https://git-scm.com/downloads)** and **[GitHub CLI](https://cli.github.com/)** (`gh`).
- **Java JDK 17 or 21** (the lab covers an upgrade path from Java 8 → 17+).
- **[Maven 3.6+](https://maven.apache.org/install.html)** and **[Docker Desktop](https://docs.docker.com/desktop/)** (Docker must be **running** during the lab — PostgreSQL and RabbitMQ run in containers).
- Repo access: confirm you can open `https://github.com/VeVarunSharma/java-app-modernization-workshop` in your browser, then clone:
  `git clone https://github.com/VeVarunSharma/java-app-modernization-workshop.git`

> Please notify the **BC Gov IT lead and/or Ve Sharma** *before* the workshop if you run into setup issues.

### Pre-workshop validation

Run through this short checklist on your laptop *before* the session:

- [ ] `gh auth status` reports you are logged in to GitHub.
- [ ] **Copilot CLI** is installed and authenticated: run `copilot --version`, then run
      `copilot` and verify you are signed in (use `/login` from inside the CLI if not).
- [ ] **Copilot Chat** responds in VS Code (open the Chat panel and ask any question).
- [ ] In VS Code Settings, **`chat.extensionTools.enabled` is `true`** (the App
      Modernization extension uses agent tools).
- [ ] The **GitHub Copilot App Modernization** pane opens in the VS Code Activity Bar.
- [ ] Repo opens successfully:
      `git clone https://github.com/VeVarunSharma/java-app-modernization-workshop.git && code java-app-modernization-workshop`.
- [ ] **Docker is running:** `docker version` returns both Client and Server info.
- [ ] Java project builds locally:
  ```bash
  # macOS / Linux
  cd asset-manager && ./mvnw -q -DskipTests package
  ```
  ```cmd
  REM Windows (Command Prompt)
  cd asset-manager
  mvnw.cmd -q -DskipTests package
  ```
  ```powershell
  # Windows (PowerShell)
  cd asset-manager
  .\mvnw.cmd -q -DskipTests package
  ```

> **Facilitator-only Azure preflight (Phase 5 demo):** if you plan to demo
> containerization + deployment live, also confirm:
> - `az login` works against the demo subscription.
> - The target resource group exists (or you have permission to create one) and there is enough quota in the chosen region for Azure Container Apps / AKS.
> - Any required Azure service registrations (e.g., Container Apps, PostgreSQL Flexible Server) are enabled on the subscription.

---

## 📞 Need help?

Reach out **before the workshop** if any of the validation steps fail:

- **Ve Sharma** (facilitator) — primary contact
- Your **BC Gov IT lead**

For deeper questions during the lab, use Copilot Chat itself to debug — that is itself part of the learning.
