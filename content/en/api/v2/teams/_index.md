---
title: Teams
description: 'Create, update, delete and retrieve your organizations Teams.'
actions:
  GetTeams:
    description: >-
      Get all teams for the requesting user's organization. If the
      `include[users]` query parameter is provided, the included attribute will
      contain the users related to these teams.
    summary: Get a list of all teams
    responses:
      '200':
        description: OK
        schema_description: Response with a list of team payloads.
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
  CreateTeam:
    description: Creates a new team.
    summary: Create a new team
    responses:
      '201':
        description: CREATED
        schema_description: Response with a team payload.
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
    request_description: Teams Payload.
    request_schema_description: Create request with a team payload.
  DeleteTeam:
    description: Deletes an existing team.
    summary: Delete an existing team
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
  GetTeam:
    description: >-
      Get details of a team. If the `include[users]` query parameter is
      provided, the included attribute will contain the users related to these
      teams.
    summary: Get details of a team
    responses:
      '200':
        description: OK
        schema_description: Response with a team payload.
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
  UpdateTeam:
    description: >-
      Updates an existing team. Only provide the attributes which should be
      updated as this request is a partial update.
    summary: Update an existing team
    responses:
      '200':
        description: OK
        schema_description: Response with a team payload.
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
    request_description: Teams Payload.
    request_schema_description: Update request with a team payload.
---
