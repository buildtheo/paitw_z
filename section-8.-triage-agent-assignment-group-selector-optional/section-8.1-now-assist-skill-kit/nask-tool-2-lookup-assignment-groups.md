---
description: >-
  A second tool will be added to the skill to gather available assignment
  groups.
---

# NASK Tool 2: Lookup assignment groups

Following the previous steps to add another script tool, this time name it **assignmentgroup**:

```javascript
(function runScript(context) {
    var groups = [];

    // Resolve the sys_id of the 'itil' group type (avoid hardcoding)
    var itilTypeSysId = '';
    var typeGR = new GlideRecord('sys_user_group_type');
    typeGR.addQuery('name', 'itil');
    typeGR.setLimit(1);
    typeGR.query();
    if (typeGR.next()) {
        itilTypeSysId = typeGR.getUniqueValue();
    }

    // Query: active=true AND (type IS EMPTY OR type CONTAINS itil)
    var gr = new GlideRecord('sys_user_group');
    gr.addActiveQuery();
    var qc = gr.addNullQuery('type');
    if (itilTypeSysId) {
        qc.addOrCondition('type', 'CONTAINS', itilTypeSysId);
    }
    gr.query();

    while (gr.next()) {
        groups.push({
            sys_id: gr.getUniqueValue(),
            name: gr.getValue('name') || '',
            description: gr.getValue('description') || ''
        });
    }

    return JSON.stringify(groups);
})(context);

```

Configuration should now look like this:

<div align="left"><figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure></div>

Again, no other configuration is needed select continue until you have added the tool. Your flow should look similar to the image below. The exact order does not matter as both scripts will execute prior to the prompt.

<div align="left"><figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure></div>

To control, check back with your prompt, the \{{inputs\}} should be blue indicating that they are matched with the tools you have added.

<div align="left"><figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure></div>
