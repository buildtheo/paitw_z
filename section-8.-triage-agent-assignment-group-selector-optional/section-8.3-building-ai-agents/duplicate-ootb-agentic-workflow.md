---
description: >-
  We want to use this OOTB Agentic Workflow, but we also want to add some small
  changes, like including our earlier created NASK skill for determining the
  assignment group for incidents.
---

# Duplicate OOTB Agentic Workflow

1\.	Open the Agentic Workflow again via the “Create and manage” tab, OR when still in the testing console click “Edit workflow”\
2\.	On the right side of the screen, you will see a button with three vertical dots, click this to Duplicate the agentic workflow:

<div align="left"><figure><img src="../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure></div>

3\.	Give your copy a name – use your imagination J&#x20;\
4\.	Change the description so it includes the fact that we want to determine the assignment group:

{% code overflow="wrap" %}
```
This agentic workflow enables fulfillers to identify the category, subcategory, service, offering, configuration item and assignment group for an incident automatically, and finally link a major incident or problem.
```
{% endcode %}

5\.	Change the list of steps as well, so that it includes an extra AI Agent to be called in the workflow:

{% code overflow="wrap" %}
```
IMPORTANT:

- The incident number is the only input required from the fulfiller — no other details are needed.
- **All four AI Agents must be executed** — none should be skipped.
- Execute all AI Agents in parallel, since there are no dependencies between them.
- **Ensure each Agent runs fully and independently**, even if previous Agents complete early or produce empty results.

1. Categorize the Incident
- Execute the "Categorize ITSM Incident AI Agent" agent.
- Purpose: Identify the appropriate category and sub-category based on incident details.

2. Classify Service, Offering, and CI
- Execute the "Classify Service and CI AI Agent" agent.
- Purpose: Determine the correct service, service offering, and configuration item (CI) for the incident.

3. Determine Assignment Group
- Execute the "Determine Assignment Group AI Agent" agent.
- Purpose: Determine the correct assignment group for the incident.

4. Link Major Incident or Problem
- Execute the "Link Major Incident or Problem AI Agent" agent.
- Purpose: Check for any related Major Incidents or Problems and link them to the current incident if a match is found.
```
{% endcode %}

6\.	Create a new Version (version 2).&#x20;

<div align="left"><figure><img src="../../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure></div>

7. Click “Save and continue”
