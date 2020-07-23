---
title: Services
description: 'Create, update, delete and retrieve your organizations services.'
actions:
  GetServices:
    description: >-
      Get all services for the requesting user's organization. If the
      `include[users]` query parameter is provided, the included attribute will
      contain the users related to these services.
    summary: Get a list of all services
    responses:
      '200':
        description: OK
        schema_description: Response with a list of service payloads.
      '400':
        description: Bad Request
        schema_description: API error response.
      '401':
        description: Unauthorized
        schema_description: API error response.
      '403':
        description: Forbidden
        schema_description: API error response.
      '404':
        description: Not Found
        schema_description: API error response.
  CreateService:
    description: Creates a new service.
    summary: Create a new service
    responses:
      '201':
        description: CREATED
        schema_description: Response with a service payload.
      '400':
        description: Bad Request
        schema_description: API error response.
      '401':
        description: Unauthorized
        schema_description: API error response.
      '403':
        description: Forbidden
        schema_description: API error response.
      '404':
        description: Not Found
        schema_description: API error response.
    request_description: Service Payload.
    request_schema_description: Create request with a service payload.
  DeleteService:
    description: Deletes an existing service.
    summary: Delete an existing service
    responses:
      '204':
        description: OK
      '400':
        description: Bad Request
        schema_description: API error response.
      '401':
        description: Unauthorized
        schema_description: API error response.
      '403':
        description: Forbidden
        schema_description: API error response.
      '404':
        description: Not Found
        schema_description: API error response.
  GetService:
    description: >-
      Get details of a service. If the `include[users]` query parameter is
      provided, the included attribute will contain the users related to these
      services
    summary: Get details of a service
    responses:
      '200':
        description: OK
        schema_description: Response with a service payload.
      '400':
        description: Bad Request
        schema_description: API error response.
      '401':
        description: Unauthorized
        schema_description: API error response.
      '403':
        description: Forbidden
        schema_description: API error response.
      '404':
        description: Not Found
        schema_description: API error response.
  UpdateService:
    description: >-
      Updates an existing service. Only provide the attributes which should be
      updated as this request is a partial update.
    summary: Update an existing service
    responses:
      '200':
        description: OK
        schema_description: Response with a service payload.
      '400':
        description: Bad Request
        schema_description: API error response.
      '401':
        description: Unauthorized
        schema_description: API error response.
      '403':
        description: Forbidden
        schema_description: API error response.
      '404':
        description: Not Found
        schema_description: API error response.
    request_description: Service Payload.
    request_schema_description: Update request with a service payload.
---
