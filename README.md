Farm Advisor Agent

A tool-using AI agent that answers crop and irrigation questions, cites its sources, and is evaluated against a test set of answers written in advance.

Status: in progress. This README describes the planned design and is updated as each part is built. Results below are filled in only once they have been measured.

Problem

Crop and irrigation advice is spread across long publications and has to be combined with current weather. General-purpose chatbots answer confidently without showing where the answer came from, and a wrong answer about watering or a crop problem can cost a season. Most AI demos in this area are never tested against known correct answers.

Objective

Build an agent that:

chooses between tools: document search over open agronomy publications, a weather lookup, and simple calculations such as crop water need;
answers with its sources shown;
declines to answer when the sources do not support one;
is measured on a test set of 50 to 100 questions whose correct answers were written before the agent was built.
How it works (planned)
Question
   |
   v
Agent (decides which tools to call, in what order)
   |-- Document search -> open agronomy publications (passages + source details)
   |-- Weather lookup  -> free weather API
   |-- Calculator      -> simple crop water-need calculation
   |
   v
Answer + sources  (or a refusal if the sources do not support an answer)
   |
   v
Logged to PostgreSQL (question, answer, tool trace, cost, time)
Tech stack
Part	Choice
Language	Python
API	FastAPI
Database	PostgreSQL
Packaging	Docker
Testing	pytest
CI	GitHub Actions
Language model	LLM API (provider to be decided)
Frontend	Plain HTML and JavaScript chat page
Evaluation

The test set contains questions of four types, each with an answer key written from first-hand agricultural knowledge:

Document-only: answerable from the publications alone
Needs weather: requires a current weather lookup
Needs calculation: requires a water-need or similar calculation
Should refuse: the sources do not support an answer
Measure	Result
Answer correctness against the answer key	Not yet measured
Share of answers supported by the cited source	Not yet measured
Tool-choice accuracy	Not yet measured
Correct refusal rate	Not yet measured
Cost and time per question	Not yet measured

Any automated judge used for scoring is validated against a hand-checked sample before its results are reported.

Scope

In scope: the three-tool agent, a document corpus for one or two crops, the evaluation harness, a FastAPI backend with logging, a simple chat page, tests, Docker, CI, and a deployed demo.

Out of scope for now: fine-tuning models, photo-based disease detection, a mobile app, user accounts, real farmer deployment, other languages, and chemical dosage advice beyond what a source states.

Roadmap
 Set up repository, environment and tooling
 Collect open agronomy documents and check licences
 Write the test set and answer key
 Document ingestion
 Retrieval tool with measured hit rate
 Agent with three tools
 Evaluation harness
 FastAPI backend and database logging
 Chat page and first results
 Failure analysis and retrieval comparison
 Refusal behaviour, tests and CI
 Deployed demo and cost benchmark
 Final write-up
Getting started

Setup instructions will be added as the project is built.

bash
git clone https://github.com/sharan1221/farm-advisor-agent.git
cd farm-advisor-agent
python -m venv .venv
source .venv/bin/activate
Data and licences

Source documents are open publications. Each source and its licence will be listed in data/SOURCES.md. No private or personal data is used.

Limitations

This is a portfolio and learning project. It is not a substitute for advice from a qualified agronomist, and its answers should not be relied on for real farming decisions without checking the cited sources.

Author

Sharanjeet, Bachelor of Information Technology student at Murdoch University Dubai. LinkedIn:- sharanjeet1221 · GitHub:- sharan1221
