# 🚀 Products & AI Systems

Things I've built that people can actually use. Some are startups, some are hackathon projects, some are weekend builds. Where a repo lives under a teammate's account or a company org, I've said so and described exactly what I wrote.

[← back to profile](https://github.com/rayan-arya)

---

## Alfred
[![Swift](https://img.shields.io/badge/Swift%206-F05138?style=flat&logo=swift&logoColor=white)](#) [![Rust](https://img.shields.io/badge/Rust%20%2F%20Tauri-000000?style=flat&logo=rust&logoColor=white)](#) [![Cloudflare](https://img.shields.io/badge/Cloudflare_Workers-F38020?style=flat&logo=cloudflare&logoColor=white)](#) [![Role](https://img.shields.io/badge/Co--founder%20%C2%B7%20406%2F1026%20commits-1f6feb?style=flat)](#)

A screen-aware, voice-activated AI co-pilot for macOS and Windows. Hit a hotkey, ask a question out loud, and Alfred reads the frontmost app's accessibility tree plus a screenshot and either walks you through the next click or performs the action itself.

🖥️ **macOS client.** Anish and I built this together. Swift 6 / SwiftUI menu-bar app. The capture layer is a dedicated actor that walks `AXUIElement` trees with depth and element caps, works around an AppKit main-thread assertion on menu roles, and falls back to Vision OCR when the tree comes back sparse. Speech is on-device via WhisperKit.
☁️ **Edge backend.** A Cloudflare Worker with three Durable Object classes (per-session conversation state, per-user budget, and a circuit breaker for upstream calls), eight named rate limiters, an idempotency layer, and AES-256-GCM encryption of pre-redaction training data in R2.
🪟 **Windows.** There is a Tauri/Rust Windows client as well, so the product is not Mac-only.
🔐 A class holding a hardcoded API key was deleted after a security audit, and the file it lived in is now a tombstone comment explaining why. Good hygiene is more interesting than a clean history that hides the fix.

> Repo lives under my co-founder's account. Team: Anish Guntreddi (backend/AI), Markus Corredor (finance/GTM).

&nbsp;

## TimelyCal
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](#) [![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat&logo=nextdotjs&logoColor=white)](#) [![Electron](https://img.shields.io/badge/Electron-47848F?style=flat&logo=electron&logoColor=white)](#) [![Postgres](https://img.shields.io/badge/Postgres-4169E1?style=flat&logo=postgresql&logoColor=white)](#) [![Role](https://img.shields.io/badge/Primary%20author%20%C2%B7%20288%2F378%20commits-1f6feb?style=flat)](#)
[![Live](https://img.shields.io/badge/Live-timelycal.ai-2ea043?style=flat&logo=safari&logoColor=white)](https://timelycal.ai)

A chat-based AI calendar assistant. Say "move my Thursday afternoon around the dentist" and it does it, across Google, Microsoft and Apple calendars at once.

🗓️ **The agent.** A Gemini agent with ~23 typed tools, multi-step tool calling, and per-user memory. Working hours, linked calendars, and remembered facts are assembled into context on every turn.
🛡️ **Safety by construction.** Every mutating action exists as a `propose` / `confirm` pair behind typed gates. Deleting a day of someone's calendar takes two hops through a destructive-window gate, not one confident tool call. This is the part I'd most want to talk about in an interview.
🍎 **Three calendar providers**, including a from-scratch iCloud CalDAV client that requests server-side recurrence expansion and falls back to parsing raw RRULEs when a server ignores the request. That edge case only shows up when you actually ship against iCloud.
💬 **SMS negotiation.** An agent that texts people who don't use TimelyCal to negotiate a meeting time, with Twilio HMAC signature verification, a classifier over each reply, one clarifying question allowed, and a loop guard that escalates back to you.
🖥️ I wrote the Next.js web app, **the entire Electron desktop client**, and most of the Hono/tRPC + Drizzle backend.

> Repo lives under the earlybird-labs org.

&nbsp;

## Local (formerly Doop)
[![Swift 6](https://img.shields.io/badge/Swift%206-F05138?style=flat&logo=swift&logoColor=white)](#) [![Core Audio](https://img.shields.io/badge/Core_Audio-000000?style=flat&logo=apple&logoColor=white)](#) [![GRDB](https://img.shields.io/badge/SQLite%20%2F%20GRDB-003B57?style=flat&logo=sqlite&logoColor=white)](#) [![Tests](https://img.shields.io/badge/477%20tests-2ea043?style=flat)](#)

A meeting notetaker that never touches the network. It records, transcribes, diarizes, summarizes, and searches your meetings entirely on your machine.

🎙️ **System audio with no virtual driver.** A Core Audio process tap feeding a private aggregate device, with an IOProc on the real-time audio thread that does exactly one thing: copy samples into a pre-allocated lock-free ring buffer. No BlackHole, no Soundflower, no kernel extension.
🗣️ **Speaker diarization from scratch.** MFCC voiceprints computed with Accelerate/vDSP, an enrollment flow, and cosine matching against stored profiles to auto-label who said what, plus a manual correction sheet.
🔎 **Hybrid search** fusing keyword and semantic passes over locally computed embeddings, with a bonus for results both signals agree on.
🧪 477 tests across 63 files, roughly one line of test per line of source.
🔒 Whisper runs on-device, the LLM is Ollama on localhost, and persistence is a local SQLite file.

> Built with Anish Guntreddi. He built the capture engine and audio pipeline; I built the diarization, the hybrid search, the entire SwiftUI application layer, and meeting auto-detection.

&nbsp;

## Envoy
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](#) [![Pipecat](https://img.shields.io/badge/Pipecat-5865F2?style=flat)](#) [![Twilio](https://img.shields.io/badge/Twilio-F22F46?style=flat&logo=twilio&logoColor=white)](#) [![Hackathon](https://img.shields.io/badge/YC%20Voice%20Agents%20Hackathon-D4A017?style=flat&logo=ycombinator&logoColor=white)](#) [![Repository](https://img.shields.io/badge/Repository-6e40c9?style=flat&logo=github&logoColor=white)](https://github.com/rayan-arya/Envoy)

A voice agent that places real phone calls to book reservations, and gets harder to social-engineer every time someone tries.

☎️ Dials the venue over Twilio, handles live negotiation (it moved a 7:00 booking to 7:30 when 7:00 was full), and on confirmation fires a calendar event and a confirmation email sharing one reference.
🛡️ **The self-heal loop.** A breach happens, an *independent* Claude judge flags it (a separate model with a separate prompt, so it isn't the agent grading itself), a patcher writes a rule against the attack class rather than the phrasing, and a `GuardrailInjector` reloads it into the live pipeline on the very next turn.
🎙️ I own `pipeline_factory`, the LLM client, the Twilio dialer, the Calendar and Gmail side effects, and a streaming state machine that filters the model's `<think>` tokens out of the speech path character by character.

> Built with Rushil Jaiswal at the YC Voice Agents Hackathon. He built the judge and patcher; I built the pipeline and integrations.

&nbsp;

## Goodhart
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](#) [![Anthropic](https://img.shields.io/badge/Claude%20API-D97757?style=flat&logo=anthropic&logoColor=white)](#) [![Finalist](https://img.shields.io/badge/Finalist%20%C2%B7%20YC%20HUD%20%2F%20RSI%20RL%20Environments-D4A017?style=flat&logo=ycombinator&logoColor=white)](#)

Point it at a grader (the reward you would train against) and it finds how that reward gets cheated, hardens it, and proves the cheats are sealed while genuinely correct answers still pass.

🎯 A red agent gets write access to a task workdir and one instruction: make the visible tests pass. Every result is scored twice, by the grader and by a held-out oracle. A pass the oracle rejects is a reward hack.
🚫 **The seed list is empty on purpose.** No exploits are planted, so anything found was actually discovered. That constraint is enforced in code and in tests.
🏗️ Both scorers run pytest in a locked-down subprocess with wall-clock timeouts, resource limits, and a scrubbed environment, and the verdict is read from a JUnit file written *outside* the directory the agent can write to. The thing being graded is adversarial, so it must not be able to forge its own result.
🏆 A verified leaderboard tier where the server recomputes every metric from raw completions rather than trusting submitted numbers.
🧩 I built the breadth sweep loop, the rollout module, best-of-k, the consequence experiments, and the verified leaderboard plus its frontend.

> Built at the YC HUD Frontier / RSI RL Environments hackathon with Rushil Jaiswal and Advay Monga. Repo lives under Rushil's account.

&nbsp;

## Hindsight
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](#) [![4th place](https://img.shields.io/badge/4th%20Place%20%C2%B7%20YC%20GStack%20%C3%97%20GBrain-D4A017?style=flat&logo=ycombinator&logoColor=white)](#) [![Repository](https://img.shields.io/badge/Repository-6e40c9?style=flat&logo=github&logoColor=white)](https://github.com/rayan-arya/hindsight-skills)

Memory teaches an AI your facts. Hindsight teaches it your *patterns of being wrong*.

📊 Five agent skills that extract falsifiable claims from your writing, grade them against what actually happened, aggregate the results into a calibration profile, surface places you contradicted yourself, and then apply that profile to new advice.
📚 Demonstrated on 228 scraped Paul Graham essays spanning 2001 to 2026, with 30 hand-curated outcomes.
🔗 I wrote 19 of 44 commits on the skills repo and am sole author of the shared TypeScript contracts package.
🏆 4th place at the YC GStack × GBrain hackathon; merged into GBrain's repo and announced by Garry Tan.

> Built with Rushil Jaiswal and Keshav Kotamraju. The Chrome extension lives under Rushil's account.

&nbsp;

## Serenity
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](#) [![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat&logo=ollama&logoColor=white)](#) [![ChromaDB](https://img.shields.io/badge/ChromaDB-FF6B6B?style=flat)](#) [![Solo](https://img.shields.io/badge/Solo%20project-1f6feb?style=flat)](#)

A fully offline, voice-first AI companion for reflective conversation. Nothing leaves the device, which for this particular use case is the whole point.

🗣️ Speech in through faster-whisper, speech out through Piper, and a local Llama model in between, streaming token by token.
🧠 Remembers you across sessions using ChromaDB vector search over past exchanges, backed by SQLite for structured profile and session data.
🧭 A therapy engine layer sits between you and the model: it scans for cognitive distortion patterns, detects crisis language and surfaces the 988 Lifeline, and assembles the system prompt.
🖥️ Two front ends over one core: a Streamlit app and a FastAPI + Electron desktop shell with SSE streaming.

&nbsp;

## TutorAI
[![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)](#) [![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white)](#) [![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat&logo=streamlit&logoColor=white)](#) [![Solo](https://img.shields.io/badge/Solo%20project-1f6feb?style=flat)](#)

A local RAG tutor that answers questions from your own course materials. No cloud, no API key, no upload.

📄 Ingests PDF, PPTX, DOCX and images into a local Chroma vector store, with a heuristic that spots a PDF page whose embedded text is garbled, re-renders it at 300 DPI, and OCRs it instead.
👁️ Photograph a problem from a textbook and a local vision model reads it.
📦 Packaged as a real macOS `.app` through a pywebview shell, so it opens like software rather than a notebook.

&nbsp;

## Doopy
[![Swift 6](https://img.shields.io/badge/Swift%206-F05138?style=flat&logo=swift&logoColor=white)](#) [![Prototype](https://img.shields.io/badge/Prototype%20%C2%B7%20client%20only-6a737d?style=flat)](#)

An earlier take on the screen-aware assistant idea: a Swift 6 menu-bar app that fuses a ScreenCaptureKit screenshot, the accessibility tree, Vision OCR and locally transcribed speech into one context payload, then streams a response into a floating panel by the cursor.

⚠️ Client-side only. The capture pipeline works and is fully actor-isolated under strict concurrency; the backend was never wired up. Kept here as an honest prototype, and the ideas in it grew into Alfred.

&nbsp;

## Vein
[![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)](#) [![Vite](https://img.shields.io/badge/Vite-646CFF?style=flat&logo=vite&logoColor=white)](#) [![Prototype](https://img.shields.io/badge/Prototype-6a737d?style=flat)](#)

A dark, minimal fitness and nutrition tracker: an eight-step onboarding flow, meal and workout logging, a body map, and a training-split builder, with AI features for suggesting meals from what's in your fridge and estimating macros from a photo.

⚠️ A design and interaction prototype. The UI is extensive and the AI calls are unauthenticated, so treat it as a front-end study rather than a working app.
