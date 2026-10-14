---
description: >-
  In this section the agentic workflow is finalized and will be tested with data
  in the ServiceNow platform
---

# Section 8.4 Finalize and test the Agentic Workflow

The last settings before we can use the Agentic Workflow need to be made. Go through the following sections of the agentic workflow:\
\-	Define security controls\
\-	Add triggers\
\-	Select channels and status

<div align="left"><figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure></div>

1\.	Define security controls:\
a.	Define user access: Allow if roles **itil**

<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

b.	Define data access:&#x20;\
i.	**User identity type**: AI user\
ii.	**AI user**: itsm.aia.worker

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

2\.	Activate the OOTB copy trigger, by selecting **Trigger is ON**:

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption></figcaption></figure>

3\.	Select channels and status: make sure **Engage via the Now Assist Panel** is switched on:

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption></figcaption></figure>

4\.	You can now **Save and test** the workflow.

In order to test the workflow, you can either create an incident, or use an existing incident in testing mode.&#x20;\
\
If everything is correct, you will see fields automatically being updated and worknotes being generated about what the AI Agents have been executing:

<figure><img src="../.gitbook/assets/image (76).png" alt=""><figcaption></figcaption></figure>

_Congratulations! You finsihed this lab section and created an Agentic Workflow including a custom AI Agent._&#x20;
