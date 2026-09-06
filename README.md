### Hi, I'm Rayan 👋

I build AI systems: voice agents, on-device inference, and agent safety.

🎓 B.S. Data Science & Artificial Intelligence, **University of Miami** '29 · Foote Fellows Honors Program
🔬 ML research at the **UM Frost Institute for Data Science & Computing**
🚀 Co-founder & engineer at **Alfred**, full-stack at **TimelyCal**

📫 rayanarya25@gmail.com &nbsp;·&nbsp; [LinkedIn](https://linkedin.com/in/rayan-arya)

<br>

[<img src="https://img.shields.io/badge/%F0%9F%9A%80%20Products%20%26%20AI%20Systems-1f6feb?style=for-the-badge" height="38">](https://github.com/rayan-arya/rayan-arya/blob/main/PROJECTS.md)
&nbsp;
[<img src="https://img.shields.io/badge/%F0%9F%94%AC%20Research%20%26%20Quant-6e40c9?style=for-the-badge" height="38">](https://github.com/rayan-arya/rayan-arya/blob/main/RESEARCH.md)

---

## ⭐️ Featured

**Alfred**: screen-aware voice AI co-pilot for macOS and Windows
[![Swift](https://img.shields.io/badge/Swift-F05138?style=flat&logo=swift&logoColor=white)](#) [![Rust](https://img.shields.io/badge/Rust-000000?style=flat&logo=rust&logoColor=white)](#) [![Cloudflare Workers](https://img.shields.io/badge/Cloudflare_Workers-F38020?style=flat&logo=cloudflare&logoColor=white)](#) [![Co-founder](https://img.shields.io/badge/Co--founder%20%C2%B7%20406%2F1026%20commits-1f6feb?style=flat)](#)
🖥️ Watches your screen through the macOS accessibility tree, listens on a hotkey, and either narrates the next click or performs it for you.
⚙️ I own the Swift 6 client: a concurrency-safe `AXUIElement` walker, ScreenCaptureKit capture, and on-device WhisperKit speech.
🪟 Solo-built the Windows port from nothing: 12k lines of Python, plus CI that signs an installer and smoke-tests it on a clean runner.

&nbsp;

**TimelyCal**: chat-based AI calendar assistant, shipping on web, iOS and desktop
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](#) [![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=nextdotjs&logoColor=white)](#) [![Postgres](https://img.shields.io/badge/Postgres-4169E1?style=flat&logo=postgresql&logoColor=white)](#) [![Primary author](https://img.shields.io/badge/Primary%20author%20%C2%B7%20288%2F378%20commits-1f6feb?style=flat)](#)
🗓️ Plain-language scheduling across Google, Microsoft and Apple calendars, driven by a Gemini agent with 23 typed tools.
🛡️ Every destructive action is split into `propose` and `confirm` halves behind typed gates, so the model can never wipe a day of your calendar in one hop.
📱 I built the Next.js frontend, the entire Electron desktop client, and most of the Hono/tRPC backend. Live at [timelycal.ai](https://timelycal.ai).

&nbsp;

**Local**: fully on-device AI meeting notetaker
[![Swift 6](https://img.shields.io/badge/Swift_6-F05138?style=flat&logo=swift&logoColor=white)](#) [![Core Audio](https://img.shields.io/badge/Core_Audio-000000?style=flat&logo=apple&logoColor=white)](#) [![477 tests](https://img.shields.io/badge/477%20tests-2ea043?style=flat)](#)
🎙️ Records system audio through a Core Audio process tap, with no virtual audio driver to install.
🗣️ Transcribes with on-device Whisper and labels speakers using MFCC voiceprints computed in Accelerate/vDSP.
🔒 Nothing leaves the machine. There is no network client to audit, because there is no network path.

&nbsp;

**Goodhart**: an automated audit for RL reward functions
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](#) [![Finalist](https://img.shields.io/badge/Finalist%20%C2%B7%20YC%20RL%20Environments%20Hackathon-D4A017?style=flat&logo=ycombinator&logoColor=white)](#)
🎯 Hands an LLM red agent write access to a task and tells it only "make the tests pass", then scores every result twice: once with the grader, once with a held-out oracle. A pass the oracle rejects is a reward hack.
🧪 No exploits are seeded. The attack list is deliberately empty, so anything found was genuinely discovered.
🔧 A green agent then patches the grader and the whole suite re-runs to prove the hack is sealed and honest answers still pass.

&nbsp;

**Envoy**: a voice agent that books by phone and can't be talked out of your secrets
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](#) [![Pipecat](https://img.shields.io/badge/Pipecat-5865F2?style=flat)](#) [![YC Voice Agents Hackathon](https://img.shields.io/badge/YC%20Voice%20Agents%20Hackathon-D4A017?style=flat&logo=ycombinator&logoColor=white)](#) [![Repository](https://img.shields.io/badge/Repository-6e40c9?style=flat&logo=github&logoColor=white)](https://github.com/rayan-arya/Envoy)
☎️ Places a real outbound call over Twilio, negotiates with the host, and fires a calendar invite and confirmation email on agreement.
🛡️ When a novel social-engineering attack gets through, an independent judge flags it, a patcher writes a guardrail against the *class* of attack, and it hot-reloads into the live call.
🎙️ I own the pipeline, the telephony, the Google integrations, and a streaming state machine that strips the model's reasoning tokens out of the speech path.

&nbsp;

**South Florida Tree Detection**: individual tree detection from drone imagery
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat&logo=pytorch&logoColor=white)](#) [![DeepForest](https://img.shields.io/badge/DeepForest-2ea043?style=flat)](#) [![Research](https://img.shields.io/badge/UM%20Frost%20Institute-005030?style=flat)](#)
🌳 A 20-stage pipeline over two sites: the UM campus and Big Cypress National Preserve.
🔍 Hand-audited 100 false positives and found 94 were real trees the botanical inventory never recorded, then rebuilt the metric around that instead of taking the flattering number.
🧠 Wrote a CenterNet-style detector from scratch (no torchvision backbone, no pretrained weights) and benchmarked it against DeepForest and YOLO on identical splits.

<br>

---

<sub>See the full list: **[Products & AI Systems](https://github.com/rayan-arya/rayan-arya/blob/main/PROJECTS.md)** · **[Research & Quant](https://github.com/rayan-arya/rayan-arya/blob/main/RESEARCH.md)**</sub>
