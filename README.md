# Java (and .NET) App Modernization Workshop

Instructor-led, hands-on labs for modernizing legacy applications with **GitHub
Copilot** — Chat, CLI, and the **App Modernization** extensions for Java and .NET.

This repo is the source of truth for app modernization workshops run by Microsoft
solution engineers. Each sample is a self-contained scenario you can run in a session
or take home as a reference.

> **Branches**
> - `main` — source projects (the "before" state).
> - `expected` — example end-state after migration.

---

## 🧑‍🏫 Workshops

This repo backs multiple cohort workshops. Each cohort gets a dedicated guide,
colocated with its primary lab folder, covering its agenda, prompts, and
pre-workshop validation.

| Cohort | Date | Guide |
|---|---|---|
| 🇨🇦 **Government of British Columbia** | May 5, 2026 | [`asset-manager/bc-gov.md`](asset-manager/bc-gov.md) |

> ### 📣 Government of BC participants — start here
>
> Open **[`asset-manager/bc-gov.md`](asset-manager/bc-gov.md)** for your full agenda, the
> Phase 1–5 lab prompts, governance/APM context, and the pre-workshop validation
> checklist. The lab itself runs out of [`asset-manager/`](asset-manager) — open that
> folder as your VS Code workspace root and the guide will be right there.
>
> **TL;DR before the session:**
> 1. Install **everything** in the [BC Gov pre-workshop requirements](asset-manager/bc-gov.md#-pre-workshop-requirements)
>    (VS Code + Copilot + Copilot Chat + **App Modernization for Java** extension,
>    Java 17/21, Maven, Docker, Git, GitHub CLI, and the standalone **Copilot CLI**).
> 2. Clone this repo: `git clone https://github.com/VeVarunSharma/java-app-modernization-workshop.git`
> 3. Run the [BC Gov pre-workshop validation checklist](asset-manager/bc-gov.md#pre-workshop-validation).
> 4. Ping **Ve Sharma** *before* the workshop if anything fails.

---

## 🧪 Choose your lab

| Lab | Stack | Modernization scenario | Time | Guide |
|---|---|---|---|---|
| **asset-manager** ⭐ | Spring Boot, AWS S3, RabbitMQ, PostgreSQL | Full end-to-end: Java 8→21, S3→Azure Blob, RabbitMQ→Service Bus, PostgreSQL→Azure DB, containerize, deploy | ~2 hr | [README](asset-manager/README.md) |
| **jakarta-ee/student-web-app** | Java EE on Open Liberty (Ant) | Ant→Maven and Java EE→**Jakarta EE 10**, Spring 5→6 | ~1 hr | [README](jakarta-ee/student-web-app/README.md) |
| **mi-sql-public-demo** | Java + Azure SQL | Replace password auth with **Managed Identity** (getting-started) | ~30 min | [README](mi-sql-public-demo/README.md) |
| **rabbitmq-sender** | Java + RabbitMQ | Author your **own custom migration formula** with Copilot | ~30 min | [README](rabbitmq-sender/README.md) |
| **todo-web-api-use-oracle-db** | Spring Boot + Oracle XE | Migrate Oracle-specific SQL/types to **Azure Database for PostgreSQL** | ~45 min | [README](todo-web-api-use-oracle-db/README.md) |
| **ContosoUniversity** | .NET Framework 4.8 + ASP.NET MVC | Local file storage → **Azure Blob Storage** with App Mod for **.NET** | ~1 hr | [README](ContosoUniversity/README.md) |
| **Malshinon** | .NET Framework 4.8 console app + MySQL | Modernize legacy .NET app and storage with App Mod for **.NET** | ~45 min | [README](Malshinon/README.md) |

⭐ = primary lab for the BC Gov cohort.

---

## 🤖 Pre-configured Copilot context (APM)

This repo ships with an [`apm.yml`](apm.yml) manifest, managed by
**[Microsoft APM](https://github.com/microsoft/apm)** (Agent Package Manager). It
pins a curated set of workshop-relevant agents and skills from
[`github/awesome-copilot`](https://github.com/github/awesome-copilot) so every
attendee gets the **same Copilot context** with one command.

The integrated files are committed under [`.github/agents/`](.github/agents/) and
[`.agents/skills/`](.agents/skills/) — meaning **Copilot in VS Code will pick them
up the moment you open the repo**, even if you haven't installed APM yet. You only
need APM to refresh, audit, or add more packages.

| Type | Package | What it brings to the workshop |
|---|---|---|
| Agent | [`modernize-java`](https://github.com/github/awesome-copilot/blob/main/agents/modernize-java.agent.md) | Incremental Java upgrades (e.g. 8/11/17 → 21, Spring Boot 2 → 3) — Phase 2/3 of the lab |
| Agent | [`azure-principal-architect`](https://github.com/github/awesome-copilot/blob/main/agents/azure-principal-architect.agent.md) | Azure Well-Architected guidance — Phase 5 cloud-readiness discussion |
| Skill | [`java-docs`](https://github.com/github/awesome-copilot/tree/main/skills/java-docs) | Javadoc best practices |
| Skill | [`java-junit`](https://github.com/github/awesome-copilot/tree/main/skills/java-junit) | JUnit 5 patterns (incl. parameterized tests) |
| Skill | [`java-refactoring-extract-method`](https://github.com/github/awesome-copilot/tree/main/skills/java-refactoring-extract-method) | Extract-method refactoring |
| Skill | [`codeql`](https://github.com/github/awesome-copilot/tree/main/skills/codeql) | Reasoning over CodeQL findings |
| Skill | [`dependabot`](https://github.com/github/awesome-copilot/tree/main/skills/dependabot) | Triaging Dependabot alerts |
| Skill | [`secret-scanning`](https://github.com/github/awesome-copilot/tree/main/skills/secret-scanning) | Handling secret-scanning hits |

**Install APM (optional, for refresh/audit):**

```bash
# macOS
brew install microsoft/apm/apm
# Linux / macOS (alternative)
curl -sSL https://aka.ms/apm-unix | sh
# Windows (PowerShell)
irm https://aka.ms/apm-windows | iex
```

**Common APM commands** *(run from the repo root)*:

```bash
apm install                  # hydrate dependencies into .github/agents/ and .agents/skills/
apm audit                    # scan installed packages for hidden-Unicode prompt-injection
apm deps tree                # show what's pinned and which commit
apm install --update         # refresh to the latest awesome-copilot, regenerates apm.lock.yaml
```

The `apm_modules/` cache is **gitignored** (it's per-machine). The
[`apm.yml`](apm.yml) manifest, [`apm.lock.yaml`](apm.lock.yaml) (with sha256
content hashes), and the integrated `.github/agents/` + `.agents/skills/`
directories are **committed** — that's how the workshop is bit-for-bit
reproducible across cohorts.

---

## ✅ Prerequisites

### Common (all labs)

- A **GitHub account** with **GitHub Copilot** access (Pro, Pro+, Business, or
  Enterprise plan).
- **[Git](https://git-scm.com/downloads)** + **[GitHub CLI](https://cli.github.com/)**.
- **[Visual Studio Code](https://code.visualstudio.com/)** 1.101+ with the **GitHub
  Copilot** and **GitHub Copilot Chat** extensions.
- *(Optional but recommended)* the standalone **[GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli)**:
  ```bash
  # macOS / Linux
  curl -fsSL https://gh.io/copilot-install | bash
  # or: brew install copilot-cli
  # Windows
  winget install GitHub.Copilot
  # cross-platform via npm
  npm install -g @github/copilot
  ```
  Then run `copilot` and complete `/login` to authenticate.

### Java track (`asset-manager`, `jakarta-ee/student-web-app`, `mi-sql-public-demo`, `rabbitmq-sender`, `todo-web-api-use-oracle-db`)

- **Java JDK 17 or 21** ([Microsoft Build of OpenJDK](https://learn.microsoft.com/en-us/java/openjdk/download)).
- **[Maven 3.6+](https://maven.apache.org/install.html)** (or Gradle wrapper 5+ for Gradle projects).
- **[Docker Desktop](https://docs.docker.com/desktop/)** for projects that spin up
  databases or message brokers locally.
- VS Code extension: **[GitHub Copilot App Modernization for Java](https://marketplace.visualstudio.com/items?itemName=vscjava.migrate-java-to-azure)**
  (also available for [IntelliJ IDEA](https://plugins.jetbrains.com/plugin/28791-github-copilot-app-modernization)).
- *(Tip)* this repo ships a **devcontainer** ([`.devcontainer/`](.devcontainer/)) with
  Java 21 + Azure CLI preinstalled — use **Dev Containers: Reopen in Container** in
  VS Code to skip local JDK setup.

### .NET track (`ContosoUniversity`, `Malshinon`)

- **[Visual Studio 2022](https://visualstudio.microsoft.com/)** 17.14.16+ with the
  *ASP.NET and web development* and *.NET desktop development* workloads.
- VS extension: **GitHub Copilot App Modernization for .NET** (search the VS
  marketplace from inside Visual Studio).

---

## 🩺 Pre-workshop validation

Run through this **before** any workshop to catch setup issues early:

- [ ] `gh auth status` reports you are logged in to GitHub.
- [ ] **Copilot CLI** is installed and authenticated: run `copilot --version`, then run
      `copilot` and verify you are signed in (use `/login` from inside the CLI if not).
- [ ] **Copilot Chat** responds in VS Code (open the Chat panel and ask any question).
- [ ] In VS Code Settings, **`chat.extensionTools.enabled` is `true`** (the App
      Modernization extension uses agent tools — your org policy may need to allow this).
- [ ] The **GitHub Copilot App Modernization** pane opens in the VS Code Activity Bar
      (and for .NET labs, the App Mod for .NET extension is installed in Visual Studio).
- [ ] You can clone and open this repo:
      `git clone https://github.com/VeVarunSharma/java-app-modernization-workshop.git && code java-app-modernization-workshop`.
- [ ] **Docker is running:** `docker version` returns both Client and Server info.
- [ ] *(Optional but recommended)* **APM** can refresh the bundled Copilot context: install
      `apm` (see [Pre-configured Copilot context](#-pre-configured-copilot-context-apm) above),
      then run `apm install` from the repo root and verify it ends with
      `Installed 8 APM dependencies` and `apm audit` reports `no issues found`.
- [ ] **Java labs:** the primary lab builds locally —
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
- [ ] **.NET labs:** the relevant `.sln` opens and restores in Visual Studio 2022.

---

## 🛡️ Governance & responsible use

When you bring Copilot into a regulated or public-sector environment, treat it like
**any other production dependency** — governed, not optional. The workshops cover
four control surfaces:

1. **Model controls** — which models are allowed, and where (IDE, GitHub.com, CLI).
2. **MCP server controls** — which tools/systems agents can reach.
3. **GitHub + Copilot admin controls** — org/team/repo enablement, policy, audit.
4. **APM — Agent Package Manager** — the open-source dependency manager for AI
   agents (`apm.yml` for instructions/skills/prompts/MCP, `apm-policy.yml` to
   constrain what an org will allow, lockfile + integrity hashes for provenance).
   Repo: <https://github.com/microsoft/apm>. **This repo dogfoods APM** — see
   [Pre-configured Copilot context (APM)](#-pre-configured-copilot-context-apm) above.

For data-handling and compliance posture, see the
[GitHub Copilot Trust Center](https://github.com/trust-center) and
[Microsoft Trust Center](https://www.microsoft.com/en-us/trust-center).

---

## 🎓 Train-the-Trainer

These workshops are designed to be **re-run internally** by the people who attend
them. A simple, repeatable rollout looks like:

| Step | Format | Audience |
|---|---|---|
| **1. Awareness** (1 hr) | Demo + Q&A | All developers / leadership |
| **2. Hands-on workshop** (half-day) | Lab from this repo | Dev teams |
| **3. Team deep dive** | Workshop tailored to a real team backlog | Single team |

**Champion model:** identify 1–2 *Copilot Champions* per team to run office hours and
curate prompts. Share reusable prompts (modernization, debugging, testing,
documentation) in an internal repo or Teams/SharePoint hub. Track success via
developer productivity, PR cycle time, code quality, and backlog reduction.

A worked example of the full Train-the-Trainer agenda is in
[`asset-manager/bc-gov.md`](asset-manager/bc-gov.md) — clone it as a starting point for your
own cohort.

---

## 🤝 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). To add a new cohort guide, drop a
markdown file next to the lab it targets (e.g. `asset-manager/<cohort>.md`) and
add a row to the **Workshops** table above.

## 📄 License

[MIT](LICENSE.md).
