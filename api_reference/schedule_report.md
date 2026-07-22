---
layout:
  width: wide
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Schedule a Report

Scheduling a report allows you to automatically run and deliver a report on a recurring basis without manually triggering it each time. Once scheduled, the report is generated at your chosen frequency and sent directly to recipients via email.

Scheduling requires two steps:

1. **Create a Saved Report** - Define the report template, object scope, and date range configuration that the scheduled report will run against each time.
2. **Create a Schedule** - Configure how often the report runs, what time it's delivered, and which recipients receive it by email.

### Step 1 - Create a Saved Report

{% openapi-operation spec="reporting-api" path="/v2.0/saved-reports" method="post" %}
[OpenAPI reporting-api](https://api.unified.com/reporting/swagger.json)
{% endopenapi-operation %}

### Step 2 - Schedule the Saved Report

Use the `saved_report_id` returned from Step 1 to create a recurring schedule.

{% openapi-operation spec="reporting-api" path="/v2.0/saved-reports/{report_id}/schedule" method="post" %}
[OpenAPI reporting-api](https://api.unified.com/reporting/swagger.json)
{% endopenapi-operation %}
