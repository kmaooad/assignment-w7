# Leanware Project

[![Join the chat at https://gitter.im/kmaooad18/assignment-w7](https://badges.gitter.im/kmaooad18/assignment-w7.svg)](https://gitter.im/kmaooad18/assignment-w7?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This week's assignment continues the preious one and adds several use cases.

## Feature and story status

When created, features and stories must have status 'New'. Status should be returned in `GET` requests. **Implementation advice**: you may use (if you want) C# enum to handle statuses in business logic, and convert enum to/from string when saving to DB or processing HTTP requests. For DB, [EF Core value converters](https://docs.microsoft.com/en-us/ef/core/modeling/value-conversions) can help to automatically convert enum/string for DbContext operations.

## Features approval

`POST /api/features/{id}/approve`

Request should move feature and all realted stories to status 'Approved'. Only 'New' feature can be approved. Status should not be allowed to change directly with PATCH update request (any such attempt should be ignored by API).

## Tags management

Tags can be renamed with `POST /api/tags/{tagName}/renameTo/{newName}`. Tags can be deleted with `DELETE /api/tags/{tagName}`. All changes to tags should affect features and stories that have these tags.

## Features filtering by tag

Features can be filtered by tag with `GET /api/features?tag={tagName}`. This request should return list of features that have specified tag.

**Implementation advice**: you may use separate explicit entity for modelling many-to-many relationship between tags and features/stories, e.g. FeatureTag and StoryTag. See [EF Core relationships](https://docs.microsoft.com/en-us/ef/core/modeling/relationships) documentation - "Many-to-many" section. When querying entities with many-to-many relationship, if you want to do it in one LINQ statement, you will need to explicitly include related entities - see [Loading Related Data](https://docs.microsoft.com/en-us/ef/core/querying/related-data). Another option is to manually query relationships first (your FeatureTag entities), and then use that data to query main entities (Features).