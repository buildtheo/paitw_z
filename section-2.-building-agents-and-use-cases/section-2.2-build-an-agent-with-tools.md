# Section 2.2 Build an Agent with Tools

1. &#x20;Open AI Agent Studio **(All > AI Agent Studio > Overview)**
2. Click the **Create and Manage** module.
3. Click on the **AI Agent** tab, then click **Add**

> I want an agent that can recommend solutions for all incidents. This agent identifies and recommends a resolution for an open and active incident being worked on by the Service Desk
>
> helping end users resolve their IT issues. It provide simple to follow steps to help users remediate their problem using a professional and business friendly tone. first it will need to get the dteails, any current similar incidents open, using the description search the KB for relevant articles to help. If there are no relevant articles, use your IT knowledge to come up with a recommended resolution based on the short description of the incident. Add resolution steps, along with any relevant similar incidents and knowledge articles, to the Additional Comments section of the incident record. When adding a comment, make sure to include a qualifier that states the comment was added by an AI Agent. Your output message to the user should be formatted to be easy to read with new line characters in a list format. Also provide your reasoning for recommending these steps.

<figure><img src="../.gitbook/assets/Unknown image (164)" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Unknown image (165)" alt=""><figcaption></figcaption></figure>



* Now scroll through the results, and see how Now Assist has filled in the AI Agent role, list of steps, and Agent name.
* You will see a “**Possible duplications found**” dialog pop up, click “**Ignore and continue**”

4. Click on “**Recommended Tools**”, a list of Suggested tools will appear, let’s select the relevant tools in this order by click on the “+” next to each tool type. Then Hit '**Save and Continue'**

**\*\*\*If you don't see the tools below when you click Recommended Tools, add each tool manually using the Add tool button and choose the exact ones listed below from the existing. The instructor can help guide you\*\*\*\***

<figure><img src="../.gitbook/assets/Unknown image (166)" alt=""><figcaption></figcaption></figure>

We are missing one tool, so let’s create the following tools by selecting the **Add tool** option from the AI agent definition:

5. Create the next tool by selecting **Add tool**:

* Select **Flow Action**
  * Select “**Add Worknote**’
  * **Name:** “Update additional comments in incident record”
  * **Description**: “Update the additional comments field in the incident record belonging to the incident that triggered this AI agent”
  * **Execution mode:** Autonomous
  * **Display output**: Yes

Under advance

* **Output transformation strategy**: Concise
* ‘**Generate messages**’ letting Now Assist fill in the responses, please feel free to customize those you prefer

6. Click **'Add'**
7. Create the next tool by selecting Add tool again:

* Select **Flow Action**
  * **Select flow action:** "Get Similar incident records"
  * **Name**: “Get Similar Incident Records”
  * **Description**: “Get similar incident records. The table is the 'incident" table”
  * **Execution mode**: Autonomous
  * **Display output**: Yes

Under advance

* **Output transformation strategy:** Concise
* ‘**Generate messages**’ letting Now Assist fill in the responses, please feel free to customize those you prefer

8. Click **Add**
9. Click **Save and Continue**
10. In Define security controls, click “**Save and continue**” on the following two steps:
    1. Define user access -> select “**Any Authenticated user**’ from the User access drop-down
    2. Define data access -> select the **Dynamic user**, search and select ‘**itil’** and “**admin”** from the approved roles
11. Next, at the Add triggers, click “**Save and continue**”.
12. Next, at the Select channels and status, see you can enable Agents to communicate via the Now Assist for Virtual Agent (via Employee center, or Service Portal), but for this example, we will NOT change the selection.
13. In the Communicate, this AI agent’s process to users, click on “**Generate messages**” letting Now assist create them for you, when the agent is ‘thinking’ and when it has completed it’s task, adjust as your prefer
14. On the Activation status area, make sure the Status toggle is set to "**On"**
15. Click **Save and Test**

    &#x20;

    **Now let’s test the agent!**

* In the Task box, enter “**Help me resolve INC0010248**” and click Continue to Test Chat response.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

We have left many of the tools to be ‘Human in the loop supervised’ to showcase the agentic thought process.

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Next, let’s move this Agent and its tools to an Agentic workflow!



