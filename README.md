<!-- ============================================================
  PROFILE README  |  repo name MUST be exactly: LorandPervizaj/LorandPervizaj
  Contribution snake needs .github/workflows/snake.yml (included).
============================================================ -->

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,12,20&height=230&section=header&text=Lorand%20Pervizaj&fontSize=62&fontColor=ffffff&fontAlignY=36&animation=fadeIn&desc=Building%20%C2%B7%20Breaking%20%C2%B7%20Rebuilding%20things%20to%20understand%20them&descSize=18&descAlignY=58" alt="header" width="100%"/>

<a href="https://github.com/LorandPervizaj">
  <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=22&duration=3200&pause=900&color=7AA2F7&center=true&vCenter=true&width=760&height=48&lines=Python+backend+%26+data+pipeline+engineer;Detection+engineering+%7C+SOC-as-Code+%7C+KQL;Azure+%C2%B7+Docker+%C2%B7+CI%2FCD+that+actually+rolls+back;Autonomous+AI+agents+with+real+guardrails" alt="typing intro"/>
</a>

<br/>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostGIS-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)

<br/>

<img src="https://img.shields.io/github/followers/LorandPervizaj?label=Followers&style=flat-square&color=7aa2f7" alt="followers"/>
<img src="https://img.shields.io/badge/Based%20in-Prishtina%2C%20Kosovo-1a1b27?style=flat-square&logo=googlemaps&logoColor=7aa2f7" alt="location"/>

</div>

---

## ⚡ About me

```python
class Lorand:
    studying   = "Computer Information Technology @ RIT Kosovo"
    background = ["blue team", "detection engineering", "KQL / Sentinel / Sysmon"]
    credential = "ISC2 Certified in Cybersecurity (CC)"
    builds     = ["data pipelines", "security automation", "AI agent systems"]
    ships_to   = "Azure"
    philosophy = "If I can't break it and rebuild it, I don't understand it."
```

- 🛡️ **Security:** I design detections from attacker behavior, not from dashboards. Signal over noise.
- 🏗️ **Backend:** Python/FastAPI services with typed schemas, migrations, tests, and gated releases.
- ☁️ **CloudOps:** immutable artifacts, OIDC auth (zero stored cloud creds), smoke tests, automatic rollback.
- 🤖 **AI:** agent loops with sandboxing, reviewer models, and human approval gates. No "just call the API" demos.

---

## 🚀 Flagship: Metrik / GroundTruth

> **Real-estate market intelligence for Prishtina.** A private research pipeline feeds a public Azure site that serves aggregated stats, each published with its sample size and confidence level.

<div align="center">

<a href="https://ca-metrik-api.livelydune-1ec3eb9a.eastus2.azurecontainerapps.io"><img src="https://img.shields.io/badge/%F0%9F%8C%90%20Live%20Site-Metrik%20on%20Azure-0078D4?style=for-the-badge" alt="live"/></a>
<a href="https://github.com/LorandPervizaj/GroundTruth"><img src="https://img.shields.io/badge/Source-GroundTruth-181717?style=for-the-badge&logo=github" alt="repo"/></a>

</div>

| 📊 Data | 🔁 Release cadence | 🧪 Quality gates | 🔒 Privacy |
|:--:|:--:|:--:|:--:|
| ~12k active listings after cross-portal dedup | Weekly, immutable, checksummed | pytest · Playwright · k6 · ruff · Trivy · gitleaks · pip-audit | Only aggregates leave the research host |

```mermaid
flowchart LR
  A[Scrapy + Playwright<br/>collectors] --> B[(PostGIS<br/>research DB)]
  B --> C[Normalize →<br/>Cross-source dedup]
  C --> D{Quality +<br/>source-health gates}
  D -- fail --> X[Run stops, no release]
  D -- pass --> E[Metrics →<br/>Release bundle + SHA256]
  E --> F[GitHub Release<br/>immutable]
  F --> G[Verify → Build image<br/>Trivy scan → ACR]
  G --> H[Azure Container Apps<br/>new revision]
  H --> I{Smoke test}
  I -- pass --> J[Live]
  I -- fail --> K[Auto-rollback to<br/>previous image]
```

<details>
<summary><b>What makes it more than a scraper</b> (click)</summary>

- **Public/private boundary enforced in code:** raw HTML, listing text, photos and contact data never leave the research host. The bundle verifier rejects any listing-level field.
- **Self-hosted Windows runner** for research, with a test that fails the build if a workflow gains a trigger that could run fork code.
- **Telegram owner bot:** `/status`, `/scrape_start`, `/scrape_stop`, plus push alerts for runs, deploys, and site activity.
- **Infra as code (Bicep)**, GitHub Actions to Azure via **OIDC**, k6 performance baselines, JSON logging, rate limiting, Sentry.
- **Crawl policy:** public pages only, robots.txt honored, rate limits, no login-gated scraping.

</details>

---

## 🔥 Vulcan Forge: autonomous AI coding agent

> Submit a task, the agent reads the repo, writes a fix, runs tests, gets **reviewed by a second LLM**, and commits. Everything runs in a network-isolated Docker sandbox.

```mermaid
flowchart TD
  U[POST /tasks] --> API[FastAPI]
  API --> S[Docker sandbox<br/>no network · 512MB · 1 CPU]
  S --> L[Agent loop<br/>read → patch → run_tests]
  L -->|tests pass| R[Reviewer agent<br/>JSON verdict]
  R -->|approved| C[Auto-commit]
  R -->|needs changes| L
  R -->|escalate / 3 cycles| H[Human approval gate]
  H -->|approve| C
  H -->|reject| RB[git rollback]
  L -->|tests got worse| G[Regression guard<br/>auto-revert]
```

`FastAPI` · `React + Vite live dashboard (SSE)` · `Groq + OpenRouter fallback` · `bring-your-own key` · `loop detection` · `rewrite protection` · `SQLite` · `Azure VM + Nginx + CI/CD`

<div align="center">
<a href="https://github.com/LorandPervizaj/Vulcan-Forge"><img src="https://img.shields.io/badge/Repo-Vulcan--Forge-181717?style=for-the-badge&logo=github" alt="vulcan"/></a>
</div>

---

## 🛡️ Security & detection engineering

<table>
<tr>
<td width="50%" valign="top">

### 🤖 Detection-Bot
**SOC-as-Code alert pipeline.** Sentinel webhook → normalize → persistent dedupe → explainable score → per-host kill-chain state machine → incident → live dashboard.

`NORMAL → EXECUTION → PERSISTENCE → EXFILTRATION`

`FastAPI` `SQLite` `React` `MITRE ATT&CK heatmap`

[**View repo →**](https://github.com/LorandPervizaj/Detection-Bot)

</td>
<td width="50%" valign="top">

### 📚 Detection Engineering Course
**8-week design-driven curriculum** I wrote: KQL, Azure control-plane telemetry, webhooks, IAM/NSG/Key Vault detections, Sysmon & LOLBins, NSG flow logs, Sentinel automation.

`KQL` `Azure Monitor` `Sentinel` `Sysmon`

[**View repo →**](https://github.com/LorandPervizaj/Detection_Engineering_Course)

</td>
</tr>
</table>

---

## 🧰 Tech stack

<div align="center">

**Languages & Backend**

<img src="https://skillicons.dev/icons?i=py,fastapi,js,html,css,bash,powershell&theme=dark" alt="langs"/>

**Data, Cloud & DevOps**

<img src="https://skillicons.dev/icons?i=postgres,sqlite,azure,docker,nginx,githubactions,git,github,linux&theme=dark" alt="infra"/>

**Frontend**

<img src="https://skillicons.dev/icons?i=react,vite&theme=dark" alt="frontend"/>

<br/>

![Scrapy](https://img.shields.io/badge/Scrapy-60A839?style=flat-square&logo=scrapy&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-189AB4?style=flat-square)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat-square&logo=ollama&logoColor=white)
![Qdrant](https://img.shields.io/badge/Qdrant-DC244C?style=flat-square)
![Alembic](https://img.shields.io/badge/Alembic-6BA81E?style=flat-square)
![uv](https://img.shields.io/badge/uv-DE5FE9?style=flat-square)
![Bicep](https://img.shields.io/badge/Bicep-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![k6](https://img.shields.io/badge/k6-7D64FF?style=flat-square&logo=k6&logoColor=white)
![KQL](https://img.shields.io/badge/KQL-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![Sentinel](https://img.shields.io/badge/Microsoft%20Sentinel-0078D4?style=flat-square&logo=microsoft&logoColor=white)
![MITRE](https://img.shields.io/badge/MITRE%20ATT%26CK-C8102E?style=flat-square)
![Trivy](https://img.shields.io/badge/Trivy-1904DA?style=flat-square&logo=aqua&logoColor=white)

</div>

---

## 📌 Featured repositories

<div align="center">

<a href="https://github.com/LorandPervizaj/GroundTruth"><img width="49%" src="https://github-readme-stats.vercel.app/api/pin/?username=LorandPervizaj&repo=GroundTruth&theme=tokyonight&hide_border=true" alt="GroundTruth"/></a>
<a href="https://github.com/LorandPervizaj/Vulcan-Forge"><img width="49%" src="https://github-readme-stats.vercel.app/api/pin/?username=LorandPervizaj&repo=Vulcan-Forge&theme=tokyonight&hide_border=true" alt="Vulcan-Forge"/></a>
<a href="https://github.com/LorandPervizaj/Detection-Bot"><img width="49%" src="https://github-readme-stats.vercel.app/api/pin/?username=LorandPervizaj&repo=Detection-Bot&theme=tokyonight&hide_border=true" alt="Detection-Bot"/></a>
<a href="https://github.com/LorandPervizaj/Detection_Engineering_Course"><img width="49%" src="https://github-readme-stats.vercel.app/api/pin/?username=LorandPervizaj&repo=Detection_Engineering_Course&theme=tokyonight&hide_border=true" alt="Detection course"/></a>

</div>

<details>
<summary><b>Learning projects</b> (ML & GenAI fundamentals)</summary>

- 🧠 [**rag-ollama-assistant**](https://github.com/LorandPervizaj/rag-ollama-assistant): fully local RAG: Ollama (llama3 + nomic-embed-text), Qdrant, FastAPI.
- 📉 [**ml-churn-predictor**](https://github.com/LorandPervizaj/ml-churn-predictor): LogReg / Random Forest / XGBoost compared by ROC-AUC, served via FastAPI + Docker.

</details>

---

## 📈 GitHub stats

<div align="center">

<img height="180" src="https://github-readme-stats.vercel.app/api?username=LorandPervizaj&show_icons=true&theme=tokyonight&hide_border=true&count_private=true&include_all_commits=true" alt="stats"/>
<img height="180" src="https://github-readme-stats.vercel.app/api/top-langs/?username=LorandPervizaj&layout=compact&theme=tokyonight&hide_border=true&langs_count=6" alt="top langs"/>

<img src="https://streak-stats.demolab.com?user=LorandPervizaj&theme=tokyonight&hide_border=true" alt="streak"/>


</div>

---

## 🐍 Contribution snake

<div align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/LorandPervizaj/LorandPervizaj/output/github-snake-dark.svg"/>
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/LorandPervizaj/LorandPervizaj/output/github-snake.svg"/>
  <img alt="contribution snake" src="https://raw.githubusercontent.com/LorandPervizaj/LorandPervizaj/output/github-snake-dark.svg"/>
</picture>
</div>

---

## 🤝 Connect

<div align="center">

<a href="https://www.linkedin.com/in/lorandpervizaj"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="linkedin"/></a>
<a href="mailto:lorand.pervizaj@gmail.com"><img src="https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white" alt="email"/></a>
<a href="https://ca-metrik-api.livelydune-1ec3eb9a.eastus2.azurecontainerapps.io"><img src="https://img.shields.io/badge/Metrik-Live-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white" alt="metrik"/></a>

<sub>Open to security, backend and data-engineering internships and collaborations.</sub>

<br/><br/>

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,12,20&height=120&section=footer" alt="footer" width="100%"/>

</div>
