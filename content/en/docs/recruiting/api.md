---
title: "MindKey Recruiting API"
description: "MindKey recruiting API is a REST API and it is hosted in Azure. Our API has predictable resource-oriented URLs, accepts form-data request bodies, returns JSON, and uses standard HTTP response codes, authentication and verbs."
lead: "The recruiting API can be called from the customer’s side through the CustomerId."
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "recruiting"
weight: 120
toc: true
---

## Website Sample
MindKey can deliver a sample website that shows how to use the API. The sample site consists of 3 pages:
- A list of vacancies
- A detail page for a single vacancy
- An application form

The list for the vacancies uses the GET /vacancies/ to get information about the required vacancies while the detail page uses GET /vacancies/:id.

The page with the application form uses GET /candidates/lookups to get the data for lookups on the application form, and then POST /candidates/ to create an application in MindKey when the form is submitted.

## Authorization
There is no API keys or login needed to access the API as the API is used on publicly available site that do not require a login. Instead, we have a check on the origin header of the request against a list of allowed origins. Due to that, you need to deliver a list of allowed origins to MindKey, to be able to access the API.

## Components of a REST API request/response
A REST API request/response pair has the following five components:
- The request URI, which consists of: {URI-scheme} :// {URI-host} / {resource-path} ? {query-string}. The request URI is called separately from the request message header as a convention required by most languages or frameworks.
    - URI scheme specifies the protocol needed to transfer the request, which can be either http or https. Mindkey Recruiting API only supports https.
    - URI host indicates the IP address or the domain name of the server that hosts the REST service endpoint, which for MindKey is https://recruiting-api.mindkey.com.
    - Resource path determines the resource or resource collection. For instance, vacancies/JOB_01 can be used to get the specified properties for the vacancy.
    - Query string is optional and serves for adding simple parameters such as the location of a vacancy.
- HTTP request message header fields which are split into:
    - An enforced HTTP method that indicates the service what type of operation are requested. MindKey Recruiting REST API supports GET and POST methods.
    - Optional additional header fields, as required by the specified URI and HTTP method.
- Optional HTTP request message body fields needed for the URI AND HTTP operation.
- HTTP response message header fields, which can be separated into:
    - An HTTP status code, ranging from 2xx success codes to 4xx or 5xx error codes.
    - Optional additional header fields, supporting the request response, as the Content-type response header.
- Optional HTTP response message body fields
    - MindKey recruiting API only supports the JSON Content-type.

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
