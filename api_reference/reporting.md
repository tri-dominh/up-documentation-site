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

# Reporting API

The Reporting API enables clients to create and retrieve customized reports based on predefined report templates. When there is a report request to be exported, it might take up to 60 minutes to be finished.

#### Reporting Base URL: [https://api.unified.com/reporting](https://api.unified.com/reporting)

### Report templates

Report Templates define the structure of a report, including its sections and the metrics and dimensions displayed in each section. Templates can be provided by the Unified Reporting service or created and managed by individual companies.

{% openapi-operation spec="reporting-api" path="/v2.0/report-templates" method="get" %}
[OpenAPI reporting-api](https://api.unified.com/reporting/swagger.json)
{% endopenapi-operation %}

### Reports

A Report is generated from a selected report template and user-defined configurations, such as the desired date range and the data object to report on (Company, Initiative, Initiative Group, or Brand). Once generated, report data can be retrieved through the report retrieval endpoints.

{% openapi-operation spec="reporting-api" path="/v2.0/reports" method="post" %}
[OpenAPI reporting-api](https://api.unified.com/reporting/swagger.json)
{% endopenapi-operation %}

{% openapi-operation spec="reporting-api" path="/v2.0/reports/{report_id}" method="get" %}
[OpenAPI reporting-api](https://api.unified.com/reporting/swagger.json)
{% endopenapi-operation %}
