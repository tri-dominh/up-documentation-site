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

# PMN API

The PMN API lets clients list and retrieve the companies and brands they have access to. A company is an advertiser, agency, or brand owner on the platform. A brand belongs to a company and represents a specific product line or marketing identity.

#### PMN Base URL: [https://api.unified.com/pmn](https://api.unified.com/pmn)

### Companies

Companies are the advertisers, agencies, and brand owners you can access. List results are paginated. A single company can be retrieved by ID, including an optional lifetime date range across that company's line items.

{% openapi-operation spec="pmn-api" path="/companies" method="get" %}
[OpenAPI pmn-api](https://api.unified.com/pmn/swagger.json)
{% endopenapi-operation %}

{% openapi-operation spec="pmn-api" path="/companies/{id}" method="get" %}
[OpenAPI pmn-api](https://api.unified.com/pmn/swagger.json)
{% endopenapi-operation %}

### Brands

Brands belong to a company and represent a specific product line or marketing identity. List results are paginated. A single brand can be retrieved by ID, including an optional lifetime date range across that brand's line items.

{% openapi-operation spec="pmn-api" path="/brands" method="get" %}
[OpenAPI pmn-api](https://api.unified.com/pmn/swagger.json)
{% endopenapi-operation %}

{% openapi-operation spec="pmn-api" path="/brands/{id}" method="get" %}
[OpenAPI pmn-api](https://api.unified.com/pmn/swagger.json)
{% endopenapi-operation %}
