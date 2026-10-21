I'll pull up both postings and extract the skill keywords, then explain pre-commit.

"OpenAI Emerging Talent" is a hiring track rather than one posting, so I used its main technical role, **Software Engineer, Applied Emerging Talent (2027)**. For Anthropic I used the main **Fellows Program** posting, which covers all five workstreams.

## OpenAI — SWE, Applied Emerging Talent (2027)

**Hard skills**
- JavaScript, React, and backend languages (they use Python)
- Relational databases such as Postgres/MySQL
- Interest in AI/ML (direct experience not required)
- End-to-end feature ownership for ChatGPT and the OpenAI API
- Optimizing applications for speed and scale

**Soft skills / traits**
- Self-starter, user empathy, talking to users and designing solutions
- Cross-functional collaboration with engineers, researchers, PMs and designers
- Moving fast when work is loosely defined, with competing priorities or deadlines

**Requirements:** a BS/MS in CS, CE, or a related field (or equivalent experience), and 0–1 years of experience. Compensation is listed at $180K plus equity.

## Anthropic Fellows Program

**Must-have:** Python fluency and full-time availability

**All workstreams:** a strong technical background in CS, math, or physics; thriving in fast-paced collaborative settings; implementing ideas quickly and communicating clearly; empirical AI research; AI safety motivation.

**AI Security Fellows (closest to your background):**
- Open-source contributions to LLM- or security-adjacent repositories
- Pentesting, vulnerability research, or other offensive security work
- Reported CVEs or bug bounties
- Empirical ML research, deep learning frameworks, and experiment management
- Ownership of ambiguous technical problems; willingness to do "dirty work"

**AI Safety Fellows:** empirical ML research, working with LLMs, experience in a listed research area, and open-source contributions. The listed areas are scalable oversight, adversarial robustness/AI control, model organisms, mechanistic interpretability, and AI welfare.

**ML Systems & Performance / RL Fellows:**
- Building complex ML systems; large-scale distributed systems and HPC; training, fine-tuning, or evaluating LLMs; debugging model training
- Accelerator backends, CPU simulators, synthetic data and environment pipelines, RL environments, RL algorithms

**Economics & Societal Impacts:** empirical research methods, writing up results (including null results), translating research into policy.

**Logistics:**
- The program is 4 months full-time with a weekly stipend of $3,850 plus about $15k/month in compute.
- There is no visa sponsorship, and you need work authorization in the US, UK, or Canada.
- That April deadline has passed, but later cohorts are reviewed on a rolling basis.

## What is pre-commit?

Git can run a script automatically every time you `git commit`. This is called a **pre-commit hook**. If the script fails, the commit is blocked.

**pre-commit** is a Python tool that manages those hooks for you. In your `agentguard` repo it works like this:

- A `.pre-commit-config.yaml` file lists the checks, for example `ruff` (lint), `ruff format`, trailing whitespace, YAML validity, and secret scanning.
- `uv run pre-commit install` wires them into `.git/hooks` once.
- After that, each commit runs the checks on only your staged files. Ruff can auto-fix issues. If a fix happens, you re-stage the files and commit again.
- `pre-commit run --all-files` checks the whole repo on demand. Running the same command in CI makes CI enforce identical rules.

The payoff is that broken formatting or lint errors never reach the repo. It's also a small but real security-engineering signal on a résumé, especially if you add a secret-scanning hook like `gitleaks`.

Sources:
- [OpenAI — Software Engineer, Applied Emerging Talent (2027)](https://openai.com/careers/software-engineer-applied-emerging-talent-(2027)-san-francisco/)
- [Anthropic Fellows Program (Accel job board mirror)](https://jobs.accel.com/companies/anthropic/jobs/74068663-anthropic-fellows-program)