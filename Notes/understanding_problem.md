# Project Understanding and Product Direction

## Working title

**Agentic AI for Safety Monitoring with Construction Risk Analytics**

The title describes three connected capabilities:

- **Agentic AI:** a bounded workflow can coordinate specialized steps such as collecting task details, retrieving approved safety guidance, identifying candidate hazards, and preparing a draft assessment. Agents do not make final safety or compliance decisions.
- **Safety monitoring:** the system considers a task and changing site context, such as weather alerts or observations submitted by a worker or supervisor. Optional image/video analysis may flag visible conditions, but is not a substitute for inspection.
- **Construction risk analytics:** the system structures hazards, likelihood and severity ratings, existing controls, residual risk, and recommended actions so a competent person can review them consistently.

The title is intentionally broader than the first release. The initial deliverable should be a focused decision-support prototype, not a claim of a fully autonomous or production-certified safety system.

## Industry problem

Construction work is task- and site-specific. A work-at-height activity, excavation, lifting operation, or material-handling task can expose workers to different hazards; weather, equipment movement, access routes, and work sequencing can also change during a shift. A generic checklist may not capture the exact task and current conditions, while a free-form assessment can be difficult to review consistently.

The project addresses this workflow problem: help a site supervisor or safety professional prepare and update a structured, task-based risk assessment, identify missing information, and bring relevant hazards and controls to the attention of a competent reviewer. It should support Indian construction-site practices and requirements. Do not claim that it prevents accidents, ensures worker safety, or guarantees legal compliance.

## Problem statement

Develop an India-focused decision-support application that takes a defined construction task and its known site conditions, organizes the task into steps, identifies candidate hazards from an approved knowledge source, and prepares a transparent draft risk assessment with initial and residual risk ratings and suggested controls. The draft must show its assumptions and sources, flag missing or uncertain information, and require review and approval by an authorized, competent person before it is used on site.

## Intended users and operational scenario

- **Primary user:** site supervisor or safety professional preparing a task briefing or risk assessment.
- **Reviewer:** a competent, authorized safety professional who validates hazards, ratings, controls, and any applicable permit or method-statement requirements.
- **Example workflow:** before a selected high-risk activity begins, the user enters the task, location, crew context, equipment, and current observations. The system prepares a draft, highlights relevant conditions and unanswered questions, and presents it to the reviewer. The reviewer edits, approves, rejects, or requests more information. If site conditions or the task change, the assessment is reopened for review.

The initial task (for example, work at height, lifting, or excavation) must be selected with the mentor and, ideally, an Indian construction safety professional. Implement one task end-to-end before attempting broad site-wide coverage.

## Assessment terminology

Use **task-based construction safety risk assessment (HIRA/JSA-style)** as the neutral description. HIRA commonly refers to hazard identification and risk assessment; JSA/JHA describes analyzing hazards associated with steps of a job/task. Terminology and required documents vary by employer, project, state, and applicable Indian requirements. Do not present any acronym, template, or control as universally mandated without verifying the applicable requirement.

## Inputs and outputs

### Inputs

- Task name, scope, sequence/steps, work location, and planned time.
- Workers' roles/competencies, tools, plant/equipment, materials, and nearby activities.
- Site observations entered by a worker or supervisor, including relevant hazards and existing controls.
- Optional weather data queried for an Indian location, with provider, timestamp, and source limitations shown.
- Optional images/video only where permission, privacy safeguards, and appropriate reuse rights are in place.
- Approved, versioned hazard/control references and any verified project-specific procedures.

### Draft assessment output

For each task step, present:

1. Hazard and possible harm, with the evidence or reference used.
2. People or assets that may be exposed.
3. Existing controls and initial likelihood/severity or risk category.
4. Suggested additional controls, prioritized using the applicable approved hierarchy of controls.
5. Residual likelihood/severity or risk category after controls.
6. Responsible role, action status, and any review date or trigger.
7. Relevant permit, method statement, inspection, or toolbox-talk prompts where applicable and verified.
8. Assumptions, uncertainty, missing inputs, source/version, and human approval status.

Risk scales, thresholds, and required control hierarchies must be agreed with the mentor and safety reviewer. Do not let a language model silently invent or alter the scoring rules.

## Safe and realistic system behavior

- Use deterministic, documented logic for risk-score calculation once a reviewer-approved matrix is selected.
- Use AI to assist with drafting, retrieval, summarization, and flagging candidate hazards; show references and distinguish suggestions from verified requirements.
- Ask for missing details instead of presenting a confident assessment from incomplete input.
- Require human review and explicit approval; preserve edits, source versions, timestamps, and approval history.
- Treat image/video findings as uncertain observations. A model may miss hazards or misclassify PPE, so visual alerts require confirmation.
- Do not issue stop-work commands, certify compliance, or make employment/disciplinary decisions in the prototype.

## Suggested implementation plan for an eight-week internship

1. **Weeks 1-2: Define scope and validate the workflow.** Confirm one Indian construction task with the mentor/reviewer; map user roles, task steps, output template, risk matrix, applicable references, and privacy expectations. Record unresolved regulatory questions rather than guessing.
2. **Weeks 2-3: Build a small, reviewed knowledge base.** Store task hazards, control suggestions, definitions, and source metadata in a structured format. Verify the source, jurisdiction, version, and license for every reference. Do not use unverified U.S.-specific rules as Indian requirements.
3. **Weeks 3-4: Implement the core assessment workflow.** Capture task/site inputs; produce a structured draft; calculate risk using transparent, deterministic rules; validate outputs against typed schemas; flag missing information and uncertainty.
4. **Weeks 5-6: Add context and a focused agentic workflow.** Add Indian-location weather context if useful and clearly sourced. Add specialized agent steps only where they improve a measurable part of the workflow; keep a deterministic orchestrator, bounded tools, and human approval. Treat vision as optional unless suitable, permitted data is available.
5. **Week 7: Evaluate with reviewers and test failure cases.** Compare draft assessments with a safety professional's reference assessments. Test incomplete inputs, changing weather/site context, unsupported tasks, low-confidence retrieval, incorrect model outputs, and unavailable data sources.
6. **Week 8: Demonstrate and document.** Deliver a working prototype, architecture, sample assessments, evaluation results, limitations, data/license register, and a production-readiness gap list. Be explicit that the prototype is not yet approved for operational safety decisions.

## Evaluation

Agree acceptance criteria with the mentor and safety reviewer before testing. Useful measures include:

- Coverage of reviewer-identified critical hazards for the selected task.
- Correctness and traceability of suggested controls and source references.
- Agreement between system and reviewer risk categories under the approved matrix.
- Rate of unsupported claims, missing-input handling, and appropriate abstention.
- Reviewer time and effort compared with the existing workflow.
- For optional vision: precision/recall by class and conditions (distance, lighting, occlusion), plus false-alert rate. Evaluate on a held-out, permission-cleared dataset representative of Indian sites.

Do not optimize only for a high average score: missing a critical hazard or presenting an unsafe control must be treated as a serious failure. Report sample size, task, test conditions, and reviewer protocol.

## Prototype versus production

An eight-week internship can deliver an industry-aligned prototype and evidence of feasibility; it cannot establish production readiness by itself. Before operational deployment, an organization would need, at minimum:

- Validation across sites, tasks, shifts, weather, equipment, and user groups with qualified safety professionals.
- Formal hazard analysis, safety case, sign-off, and clear accountability for decisions.
- Verified, current, jurisdiction- and project-specific requirements, with controlled updates.
- Security, access control, audit logs, backup/recovery, monitoring, and incident response.
- Privacy and consent review for worker data, photos, and video; data minimization, retention, and deletion controls.
- Reliable offline/degraded-mode behavior and a safe fallback when models, APIs, or networks fail.
- Usability testing, training, change management, and integration approval from the site operator.

The application should be described as **production-oriented** only if it follows sound engineering practices. Do not describe it as production-ready, legally compliant, or safety-certified without the necessary independent validation and organizational approval.

## Out of scope for the first prototype

- Autonomous approval of risk assessments or legal compliance.
- General coverage of every construction task, state, regulation, or project.
- Predicting accidents or claiming that the system prevents them.
- Continuous worker surveillance, identity recognition, or disciplinary scoring.
- Dependence on unverified public incident data, unlicensed images, or unconsented site video.
- Treating gridded weather as a direct measurement of site surface conditions or equipment proximity.

## Related project notes

- See [data_sources.md](../Meeting_material/data_sources.md) for India-focused source candidates and data limitations.
- See [site_conditions.md](./site_conditions.md) for the current initial list of conditions to monitor.
