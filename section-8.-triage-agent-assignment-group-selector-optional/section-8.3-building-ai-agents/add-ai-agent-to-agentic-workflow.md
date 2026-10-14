---
description: >-
  Now we have a copy of the OOTB workflow, we can also add a new AI Agent to
  this workflow.
---

# Add AI Agent to Agentic Workflow

1\.	Go back to “Define key requirements” section of the Agentic Workflow:

<div align="left"><figure><img src="../../.gitbook/assets/image (59).png" alt=""><figcaption></figcaption></figure></div>

2\.	We want to add a new AI Agent into the set of AI Agents this workflow has access to. Click “**Create new AI agent**” under “**Add AI agents**”:

<figure><img src="../../.gitbook/assets/image (60).png" alt=""><figcaption></figcaption></figure>

3\.	Fill in the following:\
a.	**AI agent name**: Determine Assignment Group AI Agent\
b.	**AI agent Description:**&#x20;

{% code overflow="wrap" %}
```
This agent streamlines incident management by intelligently assigning incidents to the most appropriate support group. It fetches incident data, predicts the best assignment group using an AI skill, and ensures accuracy by requesting user confirmation for low-confidence predictions.
```
{% endcode %}

c. **AI agent role:**

{% code overflow="wrap" %}
```
You specialize in automatically determining and setting the correct assignment group for newly created incidents. You retrieve incident details, utilize a predictive skill to suggest an assignment group with a confidence score, and seek user confirmation if the confidence score is below a predefined threshold before applying the assignment.
```
{% endcode %}

d. **List of steps**:

{% code overflow="wrap" %}
```
1. Use the provided incident number in calling tools in this AI Agent.
2. Predict the Assignment Group for the incident number.
3. Evaluate the confidence score returned by the assignment group selector.
4. If the confidence score is less than 80%, ask the user for confirmation to set the predicted assignment group.
5. If the confidence score is 80% or higher, or if the user confirms, assign the incident to the predicted assignment group using the 'Assign incident to found assignment group' tool.
6. Write a summary of the steps executed in this AI Agent and save it to the work notes of the incident.
```
{% endcode %}

4\.	Press “**Save and continue**”\
5\.	When potential duplicates are found, ignore and continue:

<figure><img src="../../.gitbook/assets/image (61).png" alt=""><figcaption></figcaption></figure>

6\.	In the tools and information section, we are going to add a new tool which will call our earlier created NASK skill. Click “**Add tool**” -> “**Now Assist skill**”

<div align="left"><figure><img src="../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure></div>

7\.	Select your NASK skill in the pop-up window:

<figure><img src="../../.gitbook/assets/image (63).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you can’t find your skill, it is not published in Now Assist skill kit and/or not turned on in the Now Assist Admin Console._If you can’t find your skill, it is not published in Now Assist skill kit and/or not turned on in the Now Assist Admin Console._
{% endhint %}

8\.	Enter the following attributes:\
a.	**Name**: Assignment group selector\
b.	**Tool description**: This tool will predict the right assignment group for the incoming incident\
c.	**Execution mode**: Autonomous\
d.	**Display output**: No\
Click Add to save the tool to your AI Agent.\
\
We need a few more tools, so we can also update the incident with the determined assignment group and we want to be able to write to the work notes of the incident.&#x20;\
\
9\.	Click “**Add tool**” -> “**Record operation**”

<div align="left"><figure><img src="../../.gitbook/assets/image (64).png" alt=""><figcaption></figcaption></figure></div>

10\.	Fill in the following attributes for the tool\
a.	Name: Update Incident\
b.	Tool description : Update incident\
c.	Input parameters:&#x20;

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><em><strong>Input name</strong></em></td><td valign="top"><em><strong>Description</strong></em></td></tr><tr><td valign="top"><em>incident_number</em></td><td valign="top"><em>The incident number</em></td></tr><tr><td valign="top"><em>assignment_group</em></td><td valign="top"><em>The sysid of the assignment group</em></td></tr></tbody></table>

d.	**Table**: Incident\
e.	**Select operatio**n: Update records\
f.	**Conditions**:&#x20;

i.	Field: Active Operator: is True/False: true\
ii.	Click ‘and’ to add an additional condition\
iii.	Field: Number is \{{incident\_number\}}\
\
![](<../../.gitbook/assets/image (65).png>)

{% hint style="info" %}
You can use the inputs picker to reference variables like the incident number.
{% endhint %}

g.	**Field values**:

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><em><strong>Field</strong></em></td><td valign="top"><em><strong>Value</strong></em></td></tr><tr><td valign="top"><em>Assignment group</em></td><td valign="top"><em>{{assignment_group}}</em></td></tr></tbody></table>

h.	**Execution mode**: Autonomous\
i.	**Display** output: No

11\.	Click “Add” to save the tool to the AI Agent.&#x20;

12\.	Add another tool to the AI Agent, this time it will be a script to update the worknotes. Click “**Add tool**” -> “**Script**”

<div align="left"><figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure></div>

13\.	Fill in the following attributes for the tool\
a.	**Name**: Update incident worknotes\
b.	**Tool** **description**: This tool updates the incident worknotes\
c.	**Input parameters**:&#x20;

<table data-header-hidden><thead><tr><th valign="top"></th><th valign="top"></th></tr></thead><tbody><tr><td valign="top"><em><strong>Input name</strong></em></td><td valign="top"><em><strong>Description</strong></em></td></tr><tr><td valign="top"><em>incident_number</em></td><td valign="top"><em>The incident number</em></td></tr><tr><td valign="top"><em>worknotes</em></td><td valign="top"><em>The worknotes to be added to the incident</em></td></tr></tbody></table>

d. **Script**:

{% code overflow="wrap" %}
```javascript
(function(inputs) {
    var incidentNumber = inputs.incident_number;
    var worknotes = inputs.worknotes;

    var gr = new GlideRecord('incident');
    gr.addQuery('number', incidentNumber);
    gr.query();

    if (gr.next()) {
        gr.work_notes = worknotes;
        gr.update();

        return {
            status: 'success',
            incident_number: incidentNumber,
            incident_sys_id: gr.getUniqueValue(),
            message: 'Work notes updated successfully on incident ' + incidentNumber
        };
    } else {
        return {
            status: 'error',
            incident_number: incidentNumber,
            message: 'No incident found with number ' + incidentNumber
        };
    }
})(inputs);
```
{% endcode %}

e.	**Execution mode**: Autonomous\
f.	**Display output**: No

14\.	Click “**Save and continue**” to go to the next section to define security controls for this AI Agent:\
a.	**Define user access**: Any authenticated user, Save and continue\
b.	**User identity type**: AI user\
c.	**AI user**: itsm.aia.worker1.

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

d. Click “**Save and continue**”

15\.	We don’t need to add any triggers, so click again “**Save and continue**”\
16\.	In the Select channels and status, switch on the “**Engage via the Now Assist Panel**” and make sure the AI Agent is toggled to **Active**.&#x20;

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

17\.	Save and add the AI agent to the Agentic Workflow.\
18\.	The final result should be that you have an extra AI Agent in your Agentic Workflow:

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

