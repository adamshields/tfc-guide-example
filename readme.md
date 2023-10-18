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




### Ticket: Discuss Lookup Tables vs ORM-based Methods for Data Retrieval

#### Description:
The legacy 'adam' system uses lookup tables for various functionalities, which may introduce inconsistencies in data handling. This ticket aims to spark a discussion about the benefits and drawbacks of lookup tables versus using ORM to fetch and manage values directly. 

#### Objectives:

1. **Discuss Lookup Tables:**
    - Understand the existing usage of lookup tables in the legacy 'adam' system.
    - Identify the benefits and drawbacks.

2. **Discuss ORM-based Methods:**
    - Explore how ORM can be used to replace lookup tables.
    - Identify the benefits and drawbacks.
    
3. **Make a Decision:**
    - Conclude whether to continue using lookup tables, switch to ORM-based methods, or adopt a hybrid approach.

#### Lookup Tables - Potential Benefits:

- Faster read operations due to caching.
- Loose coupling between tables can offer more flexibility.
- Easier to manage business rules that don't require code changes.

#### Lookup Tables - Potential Drawbacks:

- Risk of data inconsistencies.
- Can become a bottleneck for write operations.
- Maintenance can become cumbersome as the system scales.

#### ORM-based Methods - Potential Benefits:

- Strong data consistency.
- Easier to maintain and refactor.
- More natural integration with programming languages and frameworks.

#### ORM-based Methods - Potential Drawbacks:

- May introduce some performance overhead for read operations.
- Strong coupling between tables and classes.
- Requires frequent code changes for simple rule modifications.

#### Acceptance Criteria:

- A detailed analysis of both approaches, covering their benefits and drawbacks.
- A finalized decision documented and supported by the team.

#### Additional Notes:

- Ensure that the discussion involves all key stakeholders.
- Consider the scale, performance, and business requirements.

#### Time Estimation:
- 1 week (For discussion and decision-making)
