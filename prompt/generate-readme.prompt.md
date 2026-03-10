# README.md Generator Prompt for Go Projects

## How to Use This Prompt

1. Copy the entire prompt below (starting from "---" separator)
2. Paste it into a Cursor chat session
3. The AI will analyze your Go project and either:
   - Update your existing README.md file (if one exists), preserving valuable content while adding configuration sections
   - Generate a new comprehensive README.md file (if none exists)
4. Review and customize the generated/updated README.md file as needed
5. The README.md file will be in your project's root directory

---

# Generate README.md for This Go Project

I need you to analyze this Go project and create a comprehensive README.md file that will serve as a project configuration file for Claude Code. This file should provide persistent context and guidelines for AI-assisted development.

## What is README.md?

README.md is a project configuration file that Claude Code automatically reads when placed in the root directory. It serves as authoritative system rules that define:
- Project structure and architecture
- Coding standards and conventions
- Development workflows and commands
- Testing requirements
- Security and compliance considerations
- File boundaries and constraints

## Analysis Required

Before generating or updating the README.md file, please:

1. **Check for existing README.md** - First, check if a README.md file already exists in the project root
   - If it exists, read and analyze its current content
   - Identify what sections already exist and what information is present
   - Determine what needs to be added, updated, or preserved
2. **Analyze the project structure** - Examine the directory layout, identify Go package organization patterns (cmd/, pkg/, internal/, api/, etc.)
3. **Review existing code** - Look at code style, error handling patterns, testing approaches
4. **Identify dependencies** - Check go.mod for dependencies and their purposes
5. **Examine configuration** - Look for config files, environment variables, deployment configs
6. **Review documentation** - Check existing docs, API specifications, and any other documentation files
7. **Identify healthcare-specific patterns** - Look for HIPAA compliance measures, PHI handling, security implementations

## Handling Existing README.md

If a README.md file already exists:

1. **Preserve Existing Content**: 
   - Keep all existing sections that are still relevant and accurate
   - Maintain the existing structure and formatting style if it's well-organized
   - Preserve any project-specific documentation, examples, or usage instructions

2. **Update and Enhance**:
   - Update outdated information based on current codebase analysis
   - Add missing configuration sections that are needed for Claude Code
   - Enhance existing sections with more detail where appropriate
   - Merge duplicate or overlapping sections

3. **Add Missing Sections**:
   - Add any sections from the template below that don't exist
   - Integrate new sections seamlessly with existing content
   - Ensure the document flows logically

4. **Review and Consolidate**:
   - Remove any conflicting or contradictory information
   - Ensure consistency in formatting and style throughout
   - Verify all commands and examples are accurate

If no README.md exists, create a new one following the template structure below.

## README.md Template Structure

Generate or update a README.md file with the following sections, tailored to this specific project:

### 1. Project Overview

Provide a clear description of:
- What this project does (API for healthcare claims management)
- Primary purpose and domain (healthcare claims processing)
- Key business logic and workflows
- Target users or systems that interact with it

### 2. Project Structure

Document the directory structure following Go conventions:
- **cmd/** - Main applications (if present)
- **pkg/** - Public libraries/packages (if present)
- **internal/** - Private application code (if present)
- **api/** - API definitions, OpenAPI specs, handlers (if present)
- **config/** - Configuration files (if present)
- **migrations/** - Database migrations (if present)
- **scripts/** - Utility scripts (if present)
- **docs/** - Documentation (if present)
- **test/** or **tests/** - Test utilities (if present)

For each directory, explain:
- What belongs there
- Naming conventions
- Organization patterns

### 3. Coding Standards

Specify Go coding standards to follow:

- **Formatting**: Use `gofmt` or `goimports` - code must be formatted before commit
- **Style Guide**: Follow [Effective Go](https://go.dev/doc/effective_go) and [Go Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)
- **Linting**: Use `golangci-lint` or `golint` (specify which linters are enabled)
- **Naming Conventions**:
  - Package names: lowercase, single word, no underscores
  - Exported names: Capitalized, clear and descriptive
  - Unexported names: lowercase, concise
  - Interface names: typically end with "-er" if single method
- **Error Handling**:
  - Always handle errors explicitly
  - Use `fmt.Errorf` with `%w` for error wrapping
  - Return errors, don't log and ignore
  - Provide context in error messages
- **Code Organization**:
  - Keep functions focused and small
  - Prefer composition over inheritance
  - Use interfaces for abstraction
  - Group related functionality in packages

### 4. Development Commands

List all essential development commands:

- **Setup/Installation**:
  - `go mod download` - Download dependencies
  - `go mod tidy` - Clean up dependencies
- **Building**:
  - `go build ./...` - Build all packages
  - `go build -o <binary> ./cmd/<app>` - Build specific application
- **Testing**:
  - `go test ./...` - Run all tests
  - `go test -v ./...` - Run tests with verbose output
  - `go test -race ./...` - Run tests with race detector
  - `go test -cover ./...` - Run tests with coverage
  - `go test -bench=. ./...` - Run benchmarks
- **Code Quality**:
  - `gofmt -w .` - Format all Go files
  - `goimports -w .` - Format and organize imports
  - `golangci-lint run` - Run linters
- **Documentation**:
  - `go doc <package>` - View package documentation
  - `godoc -http=:6060` - Start local documentation server
- **Dependencies**:
  - `go get <package>` - Add dependency
  - `go get -u <package>` - Update dependency
  - `go mod verify` - Verify dependencies

Include any project-specific commands (migrations, code generation, etc.)

### 5. Testing Standards

Define testing requirements:

- **Test File Naming**: `*_test.go` files alongside source files
- **Test Function Naming**: `TestXxx` for unit tests, `BenchmarkXxx` for benchmarks, `ExampleXxx` for examples
- **Testing Patterns**:
  - Use table-driven tests for multiple test cases
  - Use subtests with `t.Run()` for organized test groups
  - Use test helpers to reduce duplication
- **Test Coverage**:
  - Minimum coverage requirement (if any)
  - Focus on critical business logic
- **Test Data**:
  - Use test fixtures appropriately
  - Mock external dependencies
  - Use test databases or in-memory stores when needed
- **Integration Tests**:
  - How to run integration tests (if separate from unit tests)
  - Test environment setup requirements

### 6. API Documentation

If this is an API project, document:

- **API Specification Format**: OpenAPI/Swagger, gRPC, GraphQL, etc.
- **API Documentation Location**: Where specs are stored
- **Endpoint Conventions**:
  - URL patterns and routing
  - HTTP method usage
  - Request/response formats
- **API Versioning**: How versions are handled
- **Authentication/Authorization**: How auth is implemented
- **Documentation Generation**: Commands to generate/update API docs

### 7. Healthcare-Specific Considerations

Since this project manages healthcare claims, include critical healthcare compliance requirements:

- **HIPAA Compliance**:
  - PHI (Protected Health Information) must never be logged in plain text
  - All PHI access must be logged and auditable
  - Encryption requirements for data at rest and in transit
  - Access controls and authentication requirements
- **PHI Handling**:
  - How PHI is identified in the codebase
  - PHI masking/redaction requirements for logs and errors
  - PHI storage and retention policies
  - PHI transmission security requirements
- **Security Requirements**:
  - Authentication mechanisms (OAuth, JWT, etc.)
  - Authorization patterns (RBAC, ABAC, etc.)
  - Input validation and sanitization
  - SQL injection prevention
  - XSS prevention (if web-facing)
  - Rate limiting and DDoS protection
- **Audit Logging**:
  - What events must be logged (PHI access, data modifications, etc.)
  - Log format and retention requirements
  - Log storage and access controls
- **Data Privacy**:
  - Patient consent handling
  - Data minimization principles
  - Right to access/delete data (if applicable)
- **Healthcare Claims Terminology**:
  - Common terms used in the domain (claim, EOB, provider, member, etc.)
  - Business rules and validation requirements
  - Claims processing workflows

### 8. Dependencies

Document dependency management:

- **Go Version**: Minimum required Go version
- **Module Management**: How go.mod is maintained
- **Key Dependencies**: List critical dependencies and their purposes
- **Dependency Updates**: Process for updating dependencies
- **Vendor Directory**: Whether vendor/ is used and how

### 9. Configuration Management

Document configuration approach:

- **Configuration Sources**: Environment variables, config files, secrets management
- **Required Environment Variables**: List critical env vars
- **Configuration Validation**: How config is validated at startup
- **Secrets Management**: How secrets are handled (Vault, AWS Secrets Manager, etc.)
- **Environment-Specific Configs**: Dev, staging, production differences

### 10. Build and Deployment

Document build and deployment processes:

- **Build Requirements**: OS, architecture targets
- **Build Artifacts**: What gets built (binaries, Docker images, etc.)
- **CI/CD Pipeline**: How code is tested and deployed
- **Docker**: Dockerfile location and usage (if applicable)
- **Deployment Environments**: Dev, staging, production
- **Rollback Procedures**: How to rollback deployments

### 11. File Boundaries

Specify what should NOT be modified:

- **Generated Code**: Any auto-generated files (protobuf, OpenAPI clients, etc.)
- **Vendor Directory**: If using vendor/, don't modify directly
- **Migration Files**: Don't modify existing migrations (create new ones)
- **Lock Files**: go.sum should not be manually edited
- **Third-Party Code**: Any third-party code that's been included

### 12. Common Workflows

Document typical development workflows:

- **Adding a New Feature**:
  1. Create feature branch
  2. Write tests first (TDD approach, if used)
  3. Implement feature
  4. Run tests and linters
  5. Update documentation
  6. Create pull request
- **Fixing a Bug**:
  1. Reproduce and write test case
  2. Fix the bug
  3. Verify test passes
  4. Update documentation if needed
- **Refactoring**:
  - Ensure test coverage before refactoring
  - Run all tests after changes
  - Update related documentation

### 13. Error Handling Patterns

Document project-specific error handling:

- **Error Types**: Custom error types used in the project
- **Error Wrapping**: How errors are wrapped with context
- **Error Logging**: What errors are logged and how
- **Error Responses**: How API errors are formatted and returned
- **Error Recovery**: Panic recovery patterns (if any)

### 14. Logging Standards

Document logging approach:

- **Logging Library**: Which library is used (logrus, zap, etc.)
- **Log Levels**: When to use each level (DEBUG, INFO, WARN, ERROR)
- **Log Format**: JSON, structured, or plain text
- **What to Log**: Request IDs, user IDs, operation context
- **What NOT to Log**: PHI, passwords, tokens, sensitive data
- **Log Context**: How to add context to logs

### 15. Database and Data Access

If the project uses a database:

- **Database Type**: PostgreSQL, MySQL, MongoDB, etc.
- **ORM/Query Builder**: GORM, sqlx, database/sql, etc.
- **Migration Management**: How migrations are handled
- **Connection Pooling**: Configuration and best practices
- **Transaction Handling**: When and how to use transactions
- **Query Patterns**: Common query patterns and anti-patterns

## Generation Instructions

After analyzing the project (and existing README.md if present), generate or update a README.md file that:

1. **Is Specific**: Tailor every section to this actual project, not generic templates
2. **Is Actionable**: Provide concrete examples and commands that work for this project
3. **Is Complete**: Cover all relevant sections based on what exists in the project
4. **Is Accurate**: Reflect the actual code patterns, structure, and conventions found
5. **Is Healthcare-Aware**: Emphasize HIPAA compliance, PHI handling, and security throughout

## Output Format

Generate the README.md file in markdown format, ready to be saved in the project root. Use clear section headers, code blocks for commands, and bullet points for lists. Make it easy to read and reference.

---

## After Generation

Once you've generated or updated the README.md file:

1. Review it for accuracy against the actual project
2. Verify that existing valuable content was preserved (if updating an existing file)
3. Customize any sections that need project-specific details
4. Save it as `README.md` in the project root directory (overwriting if it existed)
5. Commit it to version control so the entire team benefits
6. Update it as the project evolves

The README.md file will now be automatically read by Claude Code whenever you work on this project, ensuring consistent AI assistance that follows your project's standards and requirements.

