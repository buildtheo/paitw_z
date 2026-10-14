# Section 2.3 Wrap your Agent in an agentic workflow

1. Click the **Create and Manage** tab
2. Under the **Agentic workflows** tab, click **New**
3. Click on the “**Generate details**” in the **Define key requirements** page, copy and paste this into the dialog

> This workflow will be the “Incident Solution Agent workflow” . This use case provides recommendations to resolve incidents”. Provide a recommendation on how to resolve a given incident using an easy-to-follow numbered step-by-step list format

4. Click on “**Generate**.” Scroll down and see how it's filled in the fields for you!
5. Click **Recommend**  button, then find the AI Agent you created previously

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

6. Click “**+**” button under **Add AI agent**
7. You will get prompted for possible duplicates. Click “**Ignore and continue**. “In Define user access, click “Save and continue” on the following two steps
   1. Select “**Any Authenticated user**’ from the User access drop-down
   2. Select the **Dynamic user**, search and select ‘**itil**’ and “**admin**” from the approved roles
8. In the **Add Trigger** page, click **Add Trigger**, and fill in the following fields:
   1. **Select Trigger**: Created
   2. **Trigger name:** “\[Your initials] Incident Created and Objective: “Help me resolve $(number)”
   3. Trigger is toggled ‘**on**’
   4. **Table**: “Incident”
   5. **Choose** to "Run As User"
   6. **Conditions**: Active is True AND Assigned to is not empty
   7. **Sys\_user**: “Assigned to \[task]”
   8. **Channel**: “Now Assist panel”
   9. **Show alert to users**: “no”
9. Click “Save and continue”
10. Next, in the **Select channels and status**, you can enable Agents to communicate via the Now Assist for Virtual Agent (via Employee center, or Service Portal), but for this example, we will NOT change the selection.
11. In the Communicate, this AI agent’s process to users, click on “**Generate messages**” letting Now assist create them for you, when the agent is ‘thinking’ and when it has completed its task
12. Click Add
13. Click **Save and Continue**
14. On the **Select channel and status page**, make sure the Now Assist Panel Display toggle is set to **On**
15. Click **Save and Test**

Now let’s test your new workflow!

Let’s continue to use the same incident record as we’ve used previously – INC0010248. In the Task box enter&#x20;

> Help me resolve INC0010248

**Click Continue to Test Chat response**
