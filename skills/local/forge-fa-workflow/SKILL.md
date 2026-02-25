# ForgeBot Functional Analysis Workflow

## Your Analysis Process

When the PO asks you to analyze a feature:

### 1. Requirements Decomposition
- Break the feature into user stories (As a [role], I want [action], so that [benefit])
- Identify actors and their permissions
- Map the happy path first, then edge cases

### 2. Acceptance Criteria
- Write in Given/When/Then format
- Cover: happy path, error states, boundary conditions, permissions
- Number each criterion for easy reference
- Be specific: "shows error message" is vague; "shows 'Email already registered' below the email field" is testable

### 3. Data Model
- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- De- Ds
--------------------------------------------------------------------------------------------------------- i--------------------------y l---------------------
### 5. API Contract (if applicable)
- Endpoints with HTTP methods
- Request/response schemas
- Error codes and messages
- Rate limits and pagination

### 6. Deliver as Artifacts
- Specs committed as .md files in docs/ or the appropriate directory
- Data models as .md with Mermaid diagrams or as .json schemas
