---
description: Here we create a new tool that will be used in the skill.
---

# NASK Tool 1: Lookup incident descriptions

Select the + symbol between start and your skill prompt add a tool node and tool type script.\
Give your script the exact name **LookupIncident** and write your own script, copy in the script below, ensure to not get any extra line breaks.

```javascript
(function runScript(context) {
    var incidentNumber = context.getValue('incidentnumber');

    var result = {
        short_description: '',
        description: '',
        found: false
    };

    if (!incidentNumber) {
        gs.warn('[IncidentLookup] No incident_number provided');
        return result;
    }

    var gr = new GlideRecord('incident');
    gr.addQuery('number', incidentNumber);
    gr.setLimit(1);
    gr.query();

    if (gr.next()) {
        result.short_description = gr.getValue('short_description') || '';
        result.description = gr.getValue('description') || '';
        result.found = true;
    } else {
        gs.warn('[IncidentLookup] No incident found for number=' + incidentNumber);
    }

    return result;
})(context);

```

Your configuration should now look like this:\
&#x20;

<figure><img src="../../.gitbook/assets/image (35).png" alt=""><figcaption></figcaption></figure>

No other configuration is needed you can now select continue until the tool is added.
