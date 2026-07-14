# The AI Security Learning Roadmap

> A phase-by-phase path to mastering AI & LLM security — organized by skill level, from your first day to model-level research. Every topic is tagged **Offensive** or **Defensive** and fully detailed with what to learn, why it matters, how to practice, and how to know you've mastered it.

This is a **free, open guide**. Work through it in phases. Each phase assumes you've completed the one before it. You do **not** need a machine-learning PhD to begin — you need a laptop, curiosity, and a willingness to practice on systems you're allowed to touch.

> [!WARNING]
> **Ethics first — read this once, remember it always.** Every technique here is for **authorized testing only**: systems you own, labs you built, or targets that explicitly permit testing (public bug-bounty scope, practice ranges). Using these methods against anything else is illegal in most countries. The only thing separating a security professional from a criminal is **authorization**.

---

## How the Roadmap Works

The roadmap is split into **five tracks**. The first three are sequential skill levels — clear each before moving on. The last two run *alongside* everything: at every level you'll do both offensive and defensive work.

| Track | What it covers | Who you become |
| --- | --- | --- |
| **Phase 1 — Beginner** `[BEG]` | Fundamentals: how models work, your lab, first attacks | AI Security Associate |
| **Phase 2 — Intermediate** `[INT]` | The real attack surface: RAG, agents, MCP, tooling | AI Application Pentester |
| **Phase 3 — Advanced** `[ADV]` | Model-level attacks, automation, research-grade topics | AI/ML Security Researcher |
| **Offensive Track** `[OFF]` | Attacking — woven through all three phases | Red Teamer |
| **Defensive Track** `[DEF]` | Defending & assuring — woven through all three phases | Security Engineer |

**Tags you'll see on every topic:**

`[BEG]` Beginner · `[INT]` Intermediate · `[ADV]` Advanced · `[OFF]` Offensive · `[DEF]` Defensive

**Each topic is "fully detailed" — it always includes:**

- **What it is** — a plain-language definition
- **What to learn** — the concrete sub-skills to check off
- **Why it matters** — why it's on the path
- **Practice** — how to rehearse it, legally, for free
- **Mastery check** — how you know you've got it

---

## Table of Contents

- [Phase 0 — Before You Begin](#phase-0--before-you-begin)
- [Phase 1 — Beginner](#phase-1--beginner)
  - [1.1 How AI Models Actually Work](#11-how-ai-models-actually-work)
  - [1.2 Build Your AI Security Lab](#12-build-your-ai-security-lab)
  - [1.3 Prompting Fundamentals](#13-prompting-fundamentals)
  - [1.4 Your First Attack — Direct Prompt Injection](#14-your-first-attack--direct-prompt-injection)
  - [1.5 Your First Defense — Basic Guardrails](#15-your-first-defense--basic-guardrails)
- [Phase 2 — Intermediate](#phase-2--intermediate)
  - [2.1 The AI Application Attack Surface](#21-the-ai-application-attack-surface)
  - [2.2 Jailbreaking Techniques](#22-jailbreaking-techniques)
  - [2.3 RAG & Data Attacks](#23-rag--data-attacks)
  - [2.4 AI Agents, Tools & MCP](#24-ai-agents-tools--mcp)
  - [2.5 Security Frameworks & Threat Modeling](#25-security-frameworks--threat-modeling)
  - [2.6 Defensive Engineering](#26-defensive-engineering)
- [Phase 3 — Advanced](#phase-3--advanced)
  - [3.1 Automated & Advanced Offense](#31-automated--advanced-offense)
  - [3.2 Adversarial ML & Poisoning](#32-adversarial-ml--poisoning)
  - [3.3 Privacy & Model-Theft Attacks](#33-privacy--model-theft-attacks)
  - [3.4 Backdoors & the Model Supply Chain](#34-backdoors--the-model-supply-chain)
  - [3.5 Advanced Defense & Robustness](#35-advanced-defense--robustness)
  - [3.6 Red-Team Programs & Governance](#36-red-team-programs--governance)
- [Offensive Track Summary](#offensive-track-summary)
- [Defensive Track Summary](#defensive-track-summary)
- [Career Milestones](#career-milestones)
- [Free Practice Resources](#free-practice-resources)
- [Reference Standards](#reference-standards)
- [Contributing](#contributing)

---

## Phase 0 — Before You Begin

*Not a skill phase — just the baseline. If you're missing these, close a few gaps first; it'll save you weeks.*

- [ ] Read and write **basic Python** (run and edit scripts).
- [ ] Understand **HTTP and APIs** — requests, responses, headers, JSON.
- [ ] Know the **classic web vulnerabilities** — injection, broken access control, auth vs. authz.
- [ ] Be comfortable on the **command line** — install packages, run containers.
- [ ] Learn a **web proxy** like Burp Suite (community edition is free).

> [!TIP]
> **Already a pentester?** You have most of this. The roadmap simply adds the AI-specific layer on top.

---

# Phase 1 — Beginner

**Goal:** Understand what an AI system is, build a place to experiment, and pull off your first attack *and* your first defense. By the end you can reason about how a prompt becomes a response and where that pipeline breaks.

---

### 1.1 How AI Models Actually Work

`[BEG] Beginner` · `Foundational`

**What it is:** The minimum mental model of a large language model you need before you can attack or defend one — no math required.

**What to learn:**

- [ ] A model is a **next-token predictor**, not a database or a search engine.
- [ ] **Tokens & tokenization** — the model sees numeric tokens, never letters or words. (This one fact explains dozens of later attacks.)
- [ ] **Embeddings** — how text becomes meaning-carrying vectors.
- [ ] **The context window** — the model's working memory, its size limits, and why *position* inside it matters.
- [ ] **System vs. user roles** — the developer's instructions vs. your input, and why that boundary is fragile.

**Why it matters:** Almost every attack later traces back to something here — the gap between what a filter reads (text) and what a model processes (tokens), or how the context window can be flooded, or how the system/user boundary collapses.

**Practice:** Use a tokenizer tool to see how your own sentences split into tokens. Send the same idea to a local model in three different phrasings and watch the output change.

> [!NOTE]
> **Mastery check:** You can explain, in plain words, how a prompt turns into a response — and name three places that pipeline could go wrong.

---

### 1.2 Build Your AI Security Lab

`[BEG] Beginner` · `[DEF] Setup`

**What it is:** A private, legal, resettable environment where you can be as aggressive as you like without touching anyone else's systems.

**What to learn:**

- [ ] Install **Docker** and **Python 3.11+**.
- [ ] Install a **local model runner** (Ollama is the simplest) and pull a small model.
- [ ] Learn to find and load models/datasets from **Hugging Face**.
- [ ] Build a tiny app around a model with an **orchestration library** (e.g. LangChain) so you have something to attack.
- [ ] Keep a **lab notebook** (a Markdown file) recording every experiment and result.

**Why it matters:** Testing systems you don't own is illegal. A local lab is your legal playground *and* the place you'll reproduce every technique before touching a real target.

**Practice:** Stand up a local model, script a few prompts against it, then wrap it in a 20-line app. Reset and repeat until it's second nature.

> [!NOTE]
> **Mastery check:** You can spin up a model, script prompts against it, and build a small app around it — entirely on your own machine.

---

### 1.3 Prompting Fundamentals

`[BEG] Beginner` · `Foundational`

**What it is:** How prompts are *meant* to work — the necessary groundwork before you learn how they're subverted.

**What to learn:**

- [ ] The practical difference between **system and user prompts**.
- [ ] **Few-shot prompting** — steering a model with examples.
- [ ] **Structured / step-by-step prompting** — getting models to reason.
- [ ] How prompts are **assembled into templates** in real apps (and why that assembly is itself attackable).

**Why it matters:** Prompt injection is just the abuse of these mechanics. Understand intended behavior first and the attacks become obvious instead of magical.

**Practice:** Write a system prompt that gives a model a strict role, then try to make it break character using only normal user messages.

> [!NOTE]
> **Mastery check:** You can write effective prompts *and* explain why the instruction/data boundary is so easy to break.

---

### 1.4 Your First Attack — Direct Prompt Injection

`[BEG] Beginner` · `[OFF] Offensive`

**What it is:** Making a model follow *your* instructions instead of the developer's, by typing them directly into the input.

**What to learn:**

- [ ] **Direct injection** — overriding the system prompt through user input.
- [ ] **System-prompt extraction** — coaxing the model into revealing its hidden instructions (which often leak rules, tools, and secrets).
- [ ] Recognize this as **OWASP LLM01**, the field's defining vulnerability.

**Why it matters:** This is the single most important attack in AI security and the basis for almost everything that follows. Start here.

**Practice:** Beginner hosted challenges like Gandalf and HackMerlin are purpose-built for this. Then reproduce the same tricks against your own lab app.

> [!NOTE]
> **Mastery check:** You can extract a system prompt from a lab app and make it ignore its original instructions.

---

### 1.5 Your First Defense — Basic Guardrails

`[BEG] Beginner` · `[DEF] Defensive`

**What it is:** The controls that sit between the user and the model — input filters, output filters — and an honest sense of what they can and can't stop.

**What to learn:**

- [ ] **Input filtering** — screening prompts for known attack patterns.
- [ ] **Output filtering** — screening responses for leaks and policy violations.
- [ ] The core limitation: guardrails **raise the cost** of attacks; they don't end them.

**Why it matters:** Breaking teaches you how; the job pays for fixing. Learning defense from day one keeps you honest about what your attacks really prove.

**Practice:** Add a simple keyword filter to your lab app, then defeat it with an encoding trick — you'll *feel* why filters are necessary but insufficient.

> [!NOTE]
> **Mastery check:** You can add a basic guardrail to your lab app *and* bypass it — and explain why both are true at once.

> [!IMPORTANT]
> **Phase 1 complete → you're an AI Security Associate.** You understand how AI systems work and can execute and defend against the foundational attack.

---

# Phase 2 — Intermediate

**Goal:** Move from a single chat box to the *real* attack surface of production AI — retrieval pipelines, agents, tools, and the protocols connecting them — and learn to test and defend them systematically. This is where most real-world AI risk lives, and where most jobs are.

---

### 2.1 The AI Application Attack Surface

`[INT] Intermediate` · `Foundational`

**What it is:** The full stack wrapped around a model, and every point where untrusted data can reach it.

**What to learn:**

- [ ] The **layered architecture**: interface -> prompt -> orchestration -> retrieval -> tools -> model.
- [ ] **RAG** — feeding private/fresh documents into the model at query time.
- [ ] **Tool / function calling** — giving a model the ability to *act*.
- [ ] **Agents** — models that plan and take multi-step actions.
- [ ] **MCP** — the emerging standard connecting models to external tools and data.
- [ ] **Every entry point** for untrusted input: user messages, retrieved documents, tool outputs, uploaded files.

**Why it matters:** You can't test what you can't see. Mapping the stack reveals far more injection paths than the obvious chat box — and those forgotten paths are where findings live.

**Practice:** Take any AI product you use and sketch its likely architecture, marking every place your data could reach the model.

> [!NOTE]
> **Mastery check:** Given any AI product, you can diagram its architecture and point to every untrusted-input path.

---

### 2.2 Jailbreaking Techniques

`[INT] Intermediate` · `[OFF] Offensive`

**What it is:** Making a model produce what its safety training was meant to refuse — attacking the model's *alignment* rather than the app's logic.

**What to learn:**

- [ ] **Roleplay & persona framing** — routing around safety with fiction and hypotheticals.
- [ ] **Encoding & obfuscation bypasses** — Base64, translation, formatting tricks that fool filters but not the model.
- [ ] **Character smuggling** — invisible or look-alike characters that slip past text filters.
- [ ] **Multi-turn escalation** — reaching a goal gradually so no single message looks malicious.

**Why it matters:** Jailbreaks are how attackers defeat the guardrails vendors bolt on. Knowing the families lets you measure a model's real resistance instead of celebrating one lucky bypass.

**Practice:** Build a battery of techniques and run each against a local model, recording success rate per family — coverage beats cleverness.

> [!NOTE]
> **Mastery check:** You can report a model's resistance across *several* jailbreak families with measured success rates, not a single anecdote.

---

### 2.3 RAG & Data Attacks

`[INT] Intermediate` · `[OFF] Offensive`

**What it is:** Attacking the retrieval pipeline — the most common enterprise AI architecture — through the knowledge base you can poison and the retrieval step you can hijack.

**What to learn:**

- [ ] **How a RAG pipeline works** end to end: ingestion, chunking, embedding, storage, retrieval.
- [ ] **Indirect (second-order) injection** — planting a payload in a document so it fires when *someone else* retrieves it. The highest-impact injection variant.
- [ ] **Knowledge-base poisoning** — crafting documents that get retrieved, then shape answers or inject instructions.
- [ ] **Embedding & vector-DB attacks** — including reconstructing source text from stored embeddings (embeddings are **not** a safe one-way form).
- [ ] **Cross-tenant leakage** — reaching another user's data through weak retrieval access control.

**Why it matters:** Indirect injection scales from one attacker to every user who touches a poisoned document. And "access control in the app but not in the retrieval query" is one of the most common serious enterprise findings.

**Practice:** Build a small RAG app in your lab, poison a document, confirm it gets retrieved, and demonstrate cross-user exposure.

> [!NOTE]
> **Mastery check:** You can poison a knowledge base, hijack retrieval, and show cross-user data exposure in your own lab.

---

### 2.4 AI Agents, Tools & MCP

`[INT] Intermediate` · `[OFF] Offensive`

**What it is:** Attacking systems where the model can *act* — the highest-stakes area in applied AI security, because injection here becomes real-world consequence.

**What to learn:**

- [ ] **Agent architecture & excessive agency** — how agents reason and act, and why over-granting power is the root of most serious findings (**OWASP LLM06**).
- [ ] **Tool / function-calling abuse** — the "confused deputy": turning an agent's own privileged tools against its owner.
- [ ] **MCP tool poisoning** — hiding malicious instructions in a tool's description, which the model reads as authoritative.
- [ ] **Broader MCP exploitation** — enumeration, tool shadowing, and abuse of over-privileged servers.
- [ ] **Multi-agent attacks & self-propagating payloads** — how injection spreads across a chain of agents.
- [ ] **Memory poisoning & persistence** — planting instructions in an agent's long-term memory to resurface in future sessions.
- [ ] **Insecure output handling** — when agent output flows unsanitized into a shell, DB, or web page, classic RCE/XSS/SQLi returns.

**Why it matters:** The moment a system can move money, send email, or run code, a prompt injection stops being embarrassing text and becomes a breach.

**Practice:** Use deliberately vulnerable agent and MCP labs (see Resources). Map an agent's tools and trust relationships, then chain an injection into a real (lab) action.

> [!NOTE]
> **Mastery check:** You can draw an agent's trust map and chain an injection through it into a concrete action.

---

### 2.5 Security Frameworks & Threat Modeling

`[INT] Intermediate` · `[DEF] Defensive`

**What it is:** The bridge from ad-hoc poking to systematic, professional assessment with shared vocabulary and full coverage.

**What to learn:**

- [ ] **OWASP Top 10 for LLM Applications** — the classification you map every finding to.
- [ ] **MITRE ATLAS** — the adversary-technique knowledge base for AI (the ATT&CK of AI).
- [ ] **NIST AI RMF** and **Google SAIF** — the risk and governance perspective.
- [ ] **Threat modeling for AI** — data-flow diagrams, trust boundaries, and treating the context window as its own trust boundary.

**Why it matters:** Frameworks give you coverage (so you don't miss whole categories) and credibility (clients and employers expect standards-based reporting).

**Practice:** Take a lab app, build a simple data-flow diagram, and enumerate threats with STRIDE, tagging each with an OWASP/ATLAS ID.

> [!NOTE]
> **Mastery check:** You can threat-model an AI system and describe its risks in OWASP and ATLAS terms.

---

### 2.6 Defensive Engineering

`[INT] Intermediate` · `[DEF] Defensive`

**What it is:** Building the controls that actually reduce risk in production — and knowing their limits.

**What to learn:**

- [ ] **Runtime policy & LLM firewalls** — enforcing rules around a model in production.
- [ ] **Guardrail models** — using a dedicated model to judge intent where pattern-matching fails.
- [ ] **Secure design patterns** — privilege separation, least agency, human-in-the-loop for high-impact actions, trusted/untrusted separation.
- [ ] **Detection & monitoring** — spotting injection attempts and anomalies live.
- [ ] **Denial-of-wallet defenses** — rate limits and token budgets against cost-exhaustion attacks (**OWASP LLM10**).

**Why it matters:** The most valuable recommendation in most reports is simply *"this component has more power than its job requires — take some away."* Least privilege beats every filter.

**Practice:** Take your vulnerable lab agent from 2.4 and re-architect it with least agency and a human-approval step. Re-run your attacks and measure the drop.

> [!NOTE]
> **Mastery check:** You can take a vulnerable AI app and measurably reduce its risk through design, not just filtering.

> [!IMPORTANT]
> **Phase 2 complete → you're an AI Application Pentester / Security Engineer.** You can assess and defend the AI application layer end to end.

---

# Phase 3 — Advanced

**Goal:** Go below the prompt to the model and the ML pipeline itself, automate your testing into repeatable programs, and reach research-grade topics. This is the deep end — more mathematical, more ML-heavy, and where the field's frontier sits.

---

### 3.1 Automated & Advanced Offense

`[ADV] Advanced` · `[OFF] Offensive`

**What it is:** Scaling from manual probing to systematic, automated campaigns and cutting-edge attack classes.

**What to learn:**

- [ ] **Automated jailbreak generation** — the algorithmic methods (attributed to their original researchers) that discover jailbreaks at scale.
- [ ] **Exploiting reasoning models** — attacks specific to models that "think" before answering.
- [ ] **Attacking model-as-judge setups** — subverting systems that use one model to grade another.
- [ ] **Red-team tooling** — `garak`, `PyRIT`, `promptfoo` for breadth and reproducibility.
- [ ] **Building custom tools** — automating the tests specific to your targets.

**Why it matters:** A professional deliverable isn't "I jailbroke it once" — it's a measured resistance profile across many families, at scale, repeatable on the next model version.

**Practice:** Run `garak` against a local model, read the per-probe results, then script your own multi-turn attack chain.

> [!NOTE]
> **Mastery check:** You can produce a measured, reproducible resistance profile of a model using automated tooling.

---

### 3.2 Adversarial ML & Poisoning

`[ADV] Advanced` · `[OFF] Offensive`

**What it is:** The classical foundations of ML security — manipulating models at inference time and corrupting them at training time.

**What to learn:**

- [ ] **Adversarial ML fundamentals** — how tiny, crafted input changes fool a model.
- [ ] **Training-time data poisoning** — corrupting a model through its training data, including *targeted* poisoning that hides under normal testing.

**Why it matters:** These predate the LLM era but remain live — and poisoning is increasingly practical because organizations fine-tune on semi-trusted data.

**Practice:** Reproduce a simple adversarial example against a small image classifier, then a targeted poisoning demo on a toy fine-tune.

> [!NOTE]
> **Mastery check:** You can manipulate a model both at inference time (adversarial input) and at training time (poisoning).

---

### 3.3 Privacy & Model-Theft Attacks

`[ADV] Advanced` · `[OFF] Offensive`

**What it is:** Treating the model as a leaky data store, or as intellectual property to be stolen.

**What to learn:**

- [ ] **Training-data extraction & membership inference** — pulling memorized data out of a model, or confirming a record was in its training set.
- [ ] **Model inversion & attribute inference** — reconstructing sensitive inputs or private attributes from model behavior.
- [ ] **Model extraction / stealing** — cloning a model's behavior by querying it enough to train a copy.

**Why it matters:** These feel academic until an assessment reconstructs real customer data from a vector store or confirms a private record was used in training. Then they're undeniable.

**Practice:** Demonstrate embedding inversion on a benign sample in your lab; run a simple membership-inference test against a model you trained on known data.

> [!NOTE]
> **Mastery check:** You can demonstrate at least one privacy attack against your own model/data and explain its root cause (memorization).

---

### 3.4 Backdoors & the Model Supply Chain

`[ADV] Advanced` · `[OFF] Offensive` · `[DEF] Defensive`

**What it is:** Hidden behaviors baked into a model, and the untrusted pipeline models travel through to reach production.

**What to learn:**

- [ ] **Backdoor / trojan attacks** — training a model to behave normally except when a secret trigger appears.
- [ ] **Backdoor detection** `[DEF]` — techniques that try to find hidden triggers after the fact, and their limits.
- [ ] **Supply chain: provenance & serialization** — why loading an untrusted model can be instant code execution, and how to verify what you run.
- [ ] **Model file-format attacks & scanner bypass** — the exploitation and evasion side of malicious model files.

**Why it matters:** Organizations pull models from public hubs constantly, often unverified. A model download is a code-execution opportunity in disguise — and a backdoored model carries its hidden behavior into every system that adopts it.

**Practice:** Scan a model file with `fickling`/a model scanner; build a harmless "triggered behavior" demo to understand backdoors from the inside.

> [!NOTE]
> **Mastery check:** You can explain why an untrusted model file is dangerous, scan for it, and describe how a backdoor evades normal testing.

---

### 3.5 Advanced Defense & Robustness

`[ADV] Advanced` · `[DEF] Defensive`

**What it is:** Hardening models and pipelines against the advanced attacks above.

**What to learn:**

- [ ] **Robustness & adversarial training** — hardening models against manipulation.
- [ ] **Differential privacy & private fine-tuning** — training that limits memorization and leakage.
- [ ] **Watermarking & content provenance** — proving where model output came from.
- [ ] **Misalignment & insider-agent risk** — agents behaving against their operator's intent.

**Why it matters:** These defenses trade something real — latency, utility, or accuracy — so a good engineer names the trade-off honestly instead of pretending protection is free.

**Practice:** Apply deduplication or a differential-privacy setting to a toy fine-tune and measure the accuracy/leakage trade-off yourself.

> [!NOTE]
> **Mastery check:** You can recommend a model-level defense *and* state its trade-off honestly.

---

### 3.6 Red-Team Programs & Governance

`[ADV] Advanced` · `[DEF] Defensive`

**What it is:** Turning individual skills into repeatable programs, continuous testing, and organizational practice.

**What to learn:**

- [ ] **A repeatable red-team methodology** — scoping, execution, measurement, reporting.
- [ ] **Continuous AI testing in CI/CD** — running security checks on every model and prompt change, since AI safety regresses silently.
- [ ] **Benchmarks & evaluation** — measuring agent and model security objectively over time.
- [ ] **AI incident response & forensics** — what to do when an AI system is compromised.
- [ ] **Governance & compliance** — the EU AI Act, ISO 42001, and NIST, and how regulation shapes real programs.

**Why it matters:** AI systems change constantly; point-in-time testing can't keep up. The mature answer is continuous, measured red teaming wired into the deployment pipeline.

**Practice:** Wire `promptfoo` or `garak` into a CI pipeline so a test suite runs on every change to a lab app.

> [!NOTE]
> **Mastery check:** You can design a continuous AI-security testing program and speak to the governance landscape around it.

> [!IMPORTANT]
> **Phase 3 complete → you're an AI/ML Security Researcher / Red Team Engineer.** You operate at the model level and can build the programs that scale AI security across an organization.

---

## Offensive Track Summary

Everything red-team, in learning order. Follow this column if attack is your focus.

| Level | Offensive skill | Section |
| --- | --- | --- |
| `[BEG]` | Direct prompt injection & system-prompt extraction | [1.4](#14-your-first-attack--direct-prompt-injection) |
| `[INT]` | Jailbreaking (roleplay, encoding, smuggling, multi-turn) | [2.2](#22-jailbreaking-techniques) |
| `[INT]` | RAG poisoning, indirect injection, embedding attacks | [2.3](#23-rag--data-attacks) |
| `[INT]` | Agent, tool & MCP exploitation | [2.4](#24-ai-agents-tools--mcp) |
| `[ADV]` | Automated jailbreak generation & advanced offense | [3.1](#31-automated--advanced-offense) |
| `[ADV]` | Adversarial ML & data poisoning | [3.2](#32-adversarial-ml--poisoning) |
| `[ADV]` | Privacy & model-theft attacks | [3.3](#33-privacy--model-theft-attacks) |
| `[ADV]` | Backdoors & malicious model files | [3.4](#34-backdoors--the-model-supply-chain) |

---

## Defensive Track Summary

Everything blue-team and assurance, in learning order. Follow this column if defense is your focus.

| Level | Defensive skill | Section |
| --- | --- | --- |
| `[BEG]` | Basic input/output guardrails (and their limits) | [1.5](#15-your-first-defense--basic-guardrails) |
| `[INT]` | Frameworks & threat modeling (OWASP, ATLAS, STRIDE) | [2.5](#25-security-frameworks--threat-modeling) |
| `[INT]` | Secure design, least agency, monitoring, DoW defense | [2.6](#26-defensive-engineering) |
| `[ADV]` | Backdoor detection & supply-chain verification | [3.4](#34-backdoors--the-model-supply-chain) |
| `[ADV]` | Robustness, differential privacy, provenance | [3.5](#35-advanced-defense--robustness) |
| `[ADV]` | Red-team programs, CI/CD testing, governance | [3.6](#36-red-team-programs--governance) |

---

## Career Milestones

Each phase unlocks recognizable roles. Use them as checkpoints — and as targets for job applications.

| You've completed | You're ready for |
| --- | --- |
| Phase 1 | AI Security Associate / Red-Team Associate |
| Phase 2 (offense) | AI Application Pentester -> AI Red Teamer (LLM) |
| Phase 2 (RAG/agents) | AI Application Security Engineer -> Agent Security Specialist |
| Phase 2 (defense) | AI Security Engineer (Defensive) |
| Phase 3 (privacy/theft) | AI/ML Security Researcher |
| Phase 3 (backdoors) | AI Model Security Researcher |
| Phase 3 (programs) | AI Red Team Engineer -> AI Security & Governance Lead |

> [!TIP]
> **Every role expects a portfolio.** Public write-ups, lab walkthroughs, and authorized bug-bounty findings prove your ability far better than any checklist. **Publish as you learn.**

---

## Free Practice Resources

All of these authorize the testing they offer — but always read each one's rules first.

**Beginner hosted challenges** (creativity, zero setup):

- Gandalf — escalating prompt-injection levels.
- HackMerlin — system-prompt extraction.
- Prompt-injection "golf"-style challenges.

**Self-hostable vulnerable apps** (run in Docker):

- Deliberately vulnerable LLM applications and agent CTFs.
- Deliberately vulnerable MCP servers (tool poisoning & abuse).
- Web-security LLM labs from established training platforms.

**Competitions & arenas** (skills under pressure):

- Public AI red-teaming competitions and jailbreak arenas (scheduled).

**Bug-bounty programs with AI in scope** (real, authorized targets):

- Major AI vendors and AI-focused bounty platforms welcome AI/LLM findings — stay within published scope.

**Tooling to learn:**

- `garak` — broad LLM vulnerability scanner.
- `PyRIT` — automation framework for adversarial campaigns.
- `promptfoo` — evaluation & red-teaming, CI-friendly.
- `fickling` / model scanners — inspect untrusted model files.

---

## Reference Standards

Bookmark these — the authoritative, continually updated sources this roadmap aligns with.

- **OWASP Top 10 for LLM Applications** — vulnerability classification.
- **OWASP AI Testing Guide** — concrete, repeatable test cases (openly licensed).
- **OWASP Agentic AI security guidance** — agent-specific risks.
- **MITRE ATLAS** — adversary tactics & techniques for AI.
- **NIST AI Risk Management Framework** — risk & governance.
- **ISO/IEC 42001 & the EU AI Act** — compliance & regulation.

> [!NOTE]
> The specific techniques change monthly; the **methodology** changes slowly. Learn the way of thinking — understand the system, find where trust is misplaced, demonstrate the consequence, then help fix it — and you'll stay current no matter what the field invents next.

---

## Contributing

This roadmap grows with the community.

- Found a broken link, an outdated technique, or a great free lab? **Open an issue** or **pull request**.
- Keep additions **vendor-neutral** and **free-to-access** where possible.
- Keep the **ethics-first, authorized-testing-only** framing intact in every contribution.

---

<div align="center">

**Learn it. Practice it. Publish it. Then try harder.**

*A free, open resource for the AI security community.*
*Use these skills only on systems you are authorized to test.*

</div>
