Migrate from Lookup Tables to DTOs in Fork Project
Description
We are transitioning from using lookup tables in the legacy Adam project to leveraging DTOs in the Fork project for better data integrity and maintainability. The migration involves modifying existing APIs and potentially altering the database schema.

Objectives
Replace all instances where lookup tables are being used with DTOs.
Ensure data integrity and consistency across all components.
Update Swagger documentation to reflect these changes.
Tasks
Audit Existing APIs: List all APIs that currently use lookup tables in the legacy Adam project.

Design DTOs: Create DTO classes that will represent the same data as the lookup tables.

Example: Replace ProjectTypeLookupTable with ProjectTypeDTO.
Update Database Schema: Assess the need for altering the database schema and perform migrations if necessary.

Modify APIs:

Update the Controllers to use DTOs instead of lookup tables.
Update the Services to populate DTOs from the underlying data.
Update the Repositories to query for the necessary data.
Test CRUD Operations: Thoroughly test all CRUD operations for these APIs to ensure that the new implementation using DTOs works as expected.

Update Documentation:

Update inline code comments.
Update Swagger annotations to document the DTOs and modified endpoints.
Review & Refactor:

Peer-review the changes for code quality, maintainability, and adherence to best practices.
Refactor code as necessary.
Performance Testing: Verify that the new implementation does not introduce any performance bottlenecks.

Deploy to Staging: Deploy the changes to the staging environment for further testing and eventual production release.

Acceptance Criteria
All APIs that used lookup tables now use DTOs.
All CRUD operations function as expected.
Swagger documentation is updated.
Code is reviewed and meets quality standards.
Additional Notes
Pay special attention to data integrity when migrating from lookup tables to DTOs.
Co-ordinate with frontend teams to ensure that these backend changes are compatible with existing or upcoming frontend implementations.
