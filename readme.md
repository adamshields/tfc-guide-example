### Ticket: Migrate `/api` Endpoints for Projects from Legacy 'adam' to 'fork'

#### Description:
Migrate all `/api` endpoints related to Projects from the legacy 'adam' system to the new 'fork' backend built on Spring. This involves ensuring that all CRUD functionalities work as expected and updating documentation to keep in sync with code changes. 

#### Objectives:

1. **Endpoint Migration:**
    - Migrate all existing API endpoints under `/api/projects` from the legacy 'adam' system to the new 'fork' Spring application.
    
2. **CRUD Functionality:**
    - Validate that Create, Read, Update, and Delete (CRUD) operations are functional for each migrated endpoint.

3. **Swagger Documentation:**
    - Update or create Swagger annotations for controllers, entities, and any other related classes or methods.
    - Ensure that documentation is sufficient for automated doc generation.

#### Acceptance Criteria:

1. **Endpoint Migration:**
    - All `/api/projects` endpoints must be fully migrated and should function as expected in the 'fork' system.

2. **CRUD Functionality:**
    - Unit tests confirm that CRUD operations for each endpoint work as expected.
    - Manual API testing (e.g., Postman) shows consistent results with the legacy system.

3. **Swagger Documentation:**
    - All relevant code has Swagger annotations.
    - Generated API documentation is accurate, comprehensive, and matches the functionality.

#### Additional Notes:

- Ensure backward compatibility where applicable.
- Test coverage should be above 80% for the new CRUD operations.
- Update any related internal documentation or README files to reflect changes.

#### Tasks:

- [ ] Code migration of `/api/projects` endpoints.
- [ ] Write unit tests for CRUD functionalities.
- [ ] Update Swagger annotations.
- [ ] Generate and review new API documentation.
- [ ] Manual testing of migrated endpoints.
  
#### Time Estimation:
- 2-3 weeks (Adjust as needed based on complexity)
