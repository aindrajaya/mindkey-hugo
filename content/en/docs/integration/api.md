---
title: "API"
description: "MindKey API is a REST API and it is hosted in Azure. Our API has predictable resource-oriented URLs, accepts JSON request bodies, returns JSON, and uses standard HTTP response codes, authentication and verbs."
lead: "MindKey API is a REST API and it is hosted in Azure. Our API has predictable resource-oriented URLs, accepts JSON request bodies, returns JSON, and uses standard HTTP response codes, authentication and verbs."
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "integration"
weight: 120
toc: true
---

## API access prerequisites:
- Local certificate and API key provided by MindKey
- List of IP numbers communicated by customers to our team
- Optional: GitHub account(s) shared by customers to our team for the upcoming API demo samples.

There are two main ways to get started with Doks:
Customers will get access to the most common parts of the data model through our API. Therefore, the samples that we provide facilitate the data reading from our data model.

Contact your primary consultant to receive more information on the local certificate and the API key. For additional information about the certificate, see Certificate renewal process.

## Tools Suggestion
- Postman
- Powershell
- Git

## Authentication
The authentication process requires a certificate and an API key. MindKey generates a new certificate that can be used locally on the developer’s machine. Next, we provide an API key that adds an increased layer of security for customers. The API key uniquely identifies the database of the customers, and together with the certificate, they represent the authenticator.

Customers need to provide the list of IP numbers that will access the API.

> Authentication
> We do not have customizable authentication for our API.

### Integration samples and PowerShell module 
You can request a Powershell or C# sample that illustrates how to use our API. The PowerShell samples use a so-called ‘shared’ module developed internally by MindKey. The module can be supplied to customers and it helps to easily make requests to the MindKey API.

## Quick start quide for your first request
The following PowerShell example describes how to obtain a list of employees in your MindKey.

## Metadata samples for controllers and get information

```
{{api_root}}/{{customer_id}}/leaveIntegrations/metadata

jSON:
{
    "entityInformation": [
        "Table: LeaveIntegration"
    ],
    "filterUpdateDelete": [
        "LeaveId",
        "EmployeeId",
        "StartDate",
        "EndDate",
        "PayrollUpdateStatus",
        "RowNumber"
    ],
    "body": [
        "columns",
        "integrationSystemName",
        "searchCondition",
        "top",
        {
            "customSearchCondition": [
                "FromDate"
            ]
        }
    ],
}
```
In the above code snippet:

- The entityInformation section explains which tables and views from MindKey are used for this controller.
- The filterUpdateDelete section describes the fields that can be used for filtering when updating or deleting records in MindKey.
- The body section always has the subsections columns, top, SearchCondition and integrationSystemName.
  - In the columns subsection, you can specify either all columns from controller using “*” or specific columns.
  - In the top subsection, a number can be specified to only return this exact number of records.
  - In the searchCondition subsection, you can specify different selection criteria. By default, criteria are AND.
  - In the integrationSystemName subsection, you can establish the names that are created in the integrationsystem setup in MindKey. The export value is returned if values for the given integrationsystem are set up in the integration exportkeys.
- In the CustomSearchCondition section, FromDate can be given and then only records created or modified after this date are returned.

## Errors
The MindKey integration API uses standard HTTP status codes. 2xx codes indicate success, 4xx codes indicate an error in the information provided, and a code in the 5xx range indicates an error on MindKey’s servers. The table below describes the common status codes.

| Error Code| Description |
| ------------- |-------------|
| 200   | The request worked as expected.    |
| 404   | The resource could not be found.     |
| 405   | Method not allowed. Encountered when using a HTTP method that is not allowed on this endpoint.     |
| 500   | Something went wrong in the MindKey API.     |
