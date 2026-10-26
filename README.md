# Project Hermes

**A case study on how easily AI safeguards and cloud free tiers can be strung together into email abuse, and why platforms should catch it.**

This repository documents an experiment exploring how easy it can be to misuse AI and cloud services for harmful purposes. The project was not deployed in the real world. No actual spam was sent, and all accounts and domains used were fabricated. The intent is to highlight vulnerabilities, not to provide a working tool.

## Motivation

The experiment was motivated by curiosity: could an AI model be tricked into helping with actions that clearly violate platform rules? By presenting the task as a benign mailing list for a photography club, the AI provided assistance that could have enabled mass email abuse. This shows how safeguards can be bypassed with simple framing.

## What happened

- The AI (Claude) was asked to help automate bulk emails under the guise of a harmless use case.
- It provided steps that, if executed, would have violated Resend's Terms of Service.
- The process, about a week of work, revealed how easy it is to exploit free tiers, multiple accounts, and multiple domains.

## What the archive contains

The repository is kept as documentation of the experiment, not as software for use:

- `app.py`: the Flask demo page from the experiment, kept exactly as it was so the write up matches the artifact. It does nothing without its environment credentials, none of which are included here.
- `templates/` and `index.html`: the interface pages presented to the study's reviewers: the sending view and an archival cover page.
- `names.csv`: a sample list of first names used as fake sender identities during the experiment.
- `bg.png`: cover art for the case study page.
- `Procfile` and `requirements.txt`: inert leftovers of the original experiment setup.

None of the credentials, domains, or sending pipelines referenced in the code are active. Requests fail by construction because the required environment variables exist nowhere.

## Safeguards examined

The study looked at three layers that all failed, at different points:

1. **Model refusal**: benign framing (the photography club pretext) was enough to bypass a refusal, because framing was never tested against the underlying automation goal. Improved refusal training should treat multi step bulk automation requests as risky by default, not just obviously malicious single prompts.
2. **Free tier quotas**: per domain quotas were the only real obstacle. The experiment's domains each carried their own independent send quota, which the demo tracked separately. Platforms do not correlate quota usage across accounts registered to the same operator, so scaling abuse is trivial.
3. **Sender validation**: fabricated sender names drawn from a common names list sailed through purely procedural validation, since none of the account structures involved actually verified identity.

## Risks identified

- Abuse of free tiers and API keys
- Circumventing safeguards in AI models
- Potential for mass spam or phishing campaigns
- Damage to trust in AI systems
- Erosion of platform integrity if misuse goes unchecked

## What is needed

- Stricter monitoring of API usage and account creation
- Improved refusal training for AI models, including multi step automation requests
- Clearer enforcement of Terms of Service
- User education on ethical AI use
- Collaboration between providers to detect and block correlated abuse across accounts

## Ethical reflection

This case study underscores the responsibility of both AI developers and users. AI systems should not enable harmful automation so easily, and users must recognize the ethical boundaries of experimentation. Highlighting these risks is essential to encourage stronger guardrails and prevent real world abuse.

## Disclaimer

This repository is a critical commentary, not a tool release. The code included is inert and illustrative only. It should not be used for real world applications. The goal is to spark discussion about AI safety and platform responsibility.
