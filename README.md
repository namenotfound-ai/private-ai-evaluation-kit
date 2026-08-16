# Private AI Evaluation Kit

A practical, vendor-neutral checklist for teams deciding whether an AI workload should stay hosted, move to a private deployment, or be built around infrastructure they control.

**Use this before you sign a long-term AI contract.** The model is only one part of the system: data boundaries, runtime, memory, tools, evaluation, operations, and exit paths determine whether the system remains useful when requirements change.

- **Live version:** [namenotfound.ai](https://namenotfound.ai)
- **Source-available model releases:** [huggingface.co/namenotfoundai](https://huggingface.co/namenotfoundai)
- **Questions / private deployment:** [ai@namenotfound.ai](mailto:ai@namenotfound.ai)

## The short version

A private AI deployment is worth evaluating when at least one of these is true:

- Sensitive data cannot be sent to a shared third-party service.
- Model outputs, adaptations, or workflow logic are part of your competitive IP.
- You need continuity across long-running work instead of isolated chat requests.
- Unit economics make repeated hosted inference expensive at your volume.
- You need to choose the hardware, runtime, release cadence, or evidence trail.
- You need a credible exit path if a vendor changes pricing, limits, or availability.

Private does **not** automatically mean better. Measure the complete system against the same workload and acceptance criteria.

## 1. Define the workload before choosing a model

Write down a representative workload, not a demo prompt.

| Dimension | Questions to answer |
|---|---|
| Inputs | What documents, code, records, images, logs, or lab data enter the system? |
| Horizon | Does the task span one prompt, one session, or months of accumulated state? |
| Actions | Does the system only answer, or must it call tools and change systems? |
| Risk | What is the cost of a wrong answer or an unverified action? |
| Latency | What is the acceptable p50/p95 response time? |
| Volume | Requests/day, tokens/request, peak concurrency, and retention period? |
| Human role | Where must a person review, approve, or correct the result? |

Create a fixed evaluation set from real or carefully de-identified work. Keep a holdout set that is never used to tune prompts or routing.

## 2. Compare ownership levels explicitly

There are at least three sensible deployment choices:

### Hosted access

Best when speed and convenience dominate. Ask for:

- data retention and training-use terms;
- region, tenant, and encryption controls;
- rate limits, model-change notice, and service-level commitments;
- export of prompts, outputs, feedback, memory, and configuration;
- a cost model that includes retries, context, tools, and storage.

### Private deployment

Best when data boundaries and operational control matter, but you still want implementation support. Ask for:

- supported hardware and minimum capacity;
- patching, monitoring, incident response, and upgrade ownership;
- what the vendor can access during support;
- reproducible deployment artifacts and rollback procedures;
- a clear boundary between vendor IP and your adaptations/data.

### Build around your infrastructure

Best when the model and surrounding system become core capability. Ask for:

- weights, source, licenses, and redistribution rights;
- runtime and kernel dependencies;
- tokenizer, prompt format, safety controls, and evaluation harness;
- how memory, retrieval, routing, and tool state are represented;
- the skills your team must own to operate it six months from now.

## 3. Demand an evidence trail

A good answer is not enough for high-value work. Require the system to record:

1. input identifiers and versions;
2. retrieved evidence and why it was selected;
3. model/runtime/version and configuration;
4. tools called, arguments, results, and failures;
5. human approvals, corrections, and overrides;
6. final output and downstream action;
7. latency, token/compute cost, and confidence signals where available.

The log should be exportable, access-controlled, tamper-evident where needed, and usable for replay.

## 4. Evaluate the system, not just the model

Run the same workload through the complete stack. Record:

- task success rate and rubric score;
- groundedness / citation accuracy;
- abstention and escalation behavior;
- tool-call correctness and recovery from failure;
- long-context retrieval quality at realistic context sizes;
- performance under concurrency;
- total cost per successful task;
- operator time per task and per incident;
- reproducibility across versions;
- data leakage and prompt-injection resistance.

A useful comparison table:

| Measure | Hosted baseline | Private candidate | Target |
|---|---:|---:|---:|
| Successful tasks |  |  |  |
| Unsupported claims |  |  |  |
| Tool errors |  |  |  |
| p95 latency |  |  |  |
| Cost / successful task |  |  |  |
| Operator minutes / task |  |  |  |
| Evidence completeness |  |  |  |

Do not let a lower per-token price hide a higher cost per **successful, reviewed** task.

## 5. Check the exit path before you need it

Put answers to these questions in writing:

- Can we export our data, memory, feedback, prompts, tools, and evaluation set?
- Can we reproduce a previous result from an archived version?
- What happens if the vendor stops supporting our hardware?
- Which parts are licensed to us, and which remain vendor-owned?
- Can we run a fallback model without rewriting the whole workflow?
- Are model updates opt-in, pinned, or silently applied?
- What are the deletion, retention, and offboarding timelines?

If the answer is "we cannot tell," treat that as a system risk—not a procurement detail.

## 6. A 30-day evaluation plan

### Days 1–5: scope

- Select one high-value, bounded workload.
- Define success, failure, escalation, and safety criteria.
- De-identify or isolate the evaluation data.
- Freeze the baseline prompts and holdout set.

### Days 6–12: baseline

- Measure the current hosted workflow end to end.
- Capture latency, cost, operator time, errors, and evidence quality.
- Document where the hosted system is already good enough.

### Days 13–22: private candidate

- Deploy in an isolated environment.
- Run the same workload and holdout set.
- Test interruption, retries, upgrades, access control, and export.
- Record compute, storage, networking, and maintenance costs.

### Days 23–30: decision

- Review results with the business owner, security, and operators.
- Choose hosted, private, hybrid, or stop.
- Write the rollback/exit plan before production approval.
- Define the next workload only if the first one met its acceptance criteria.

## 7. Questions for any vendor

1. What exactly is private: the endpoint, the runtime, the weights, the memory, or all of them?
2. Can we pin versions and reproduce outputs?
3. What happens to our data, feedback, and adaptations?
4. Which components can we inspect, export, or replace?
5. How do you verify tool use and long-running work?
6. What is the failure and recovery model?
7. What hardware do you support, and what is the real throughput at our context size?
8. What is the total cost at our volume, including operators and incidents?
9. What do we own when the contract ends?
10. Can we run the evaluation on our own representative data?

## About Name Not Found

Name Not Found builds private AI systems around the principle that organizations should be able to own the intelligence, the implementation, and the IP that their workflows create. Its public model family includes:

- **NNF-EAM** — long-context intelligence with adaptive memory, routing, retrieval, and native experts;
- **Nexum** — planning, tool use, recovery, and verified completion;
- **Nomos** — multi-agent orchestration with tools, evidence, and long-running work;
- **Nightlight** — defensive security scanning, patching, verification, and evidence trails;
- **Nucleus-Resynthesis** — scientific and quantitative reasoning;
- **Nitrous** — hardware-native inference (coming soon).

The public catalog is available on [Hugging Face](https://huggingface.co/namenotfoundai). For hosted access, private deployment, or a custom implementation conversation, contact [ai@namenotfound.ai](mailto:ai@namenotfound.ai).

## Contribute

If you improve this checklist, open a pull request with:

- the specific evaluation problem addressed;
- a source or reproducible method where applicable;
- the audience and deployment assumptions;
- any tradeoffs or failure modes.

Keep the guide vendor-neutral. A buyer should be able to use it even when Name Not Found is not the right fit.

## License

This guide is released under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). You may adapt it with attribution.
