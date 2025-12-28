INTENT:"Design and implement the application using a Monolithic Architecture, where all core components—user interface, business logic, data access, and integrations—are developed, deployed, and executed as a single unified application. This architecture is intended for small to medium-sized applications where simplicity, faster development, and ease of deployment are prioritized."
CREATE: "Create a single, cohesive application that encapsulates all features and modules within one codebase, including user-facing functionality, admin/business logic, database interactions, and third-party integrations."
BUILD:"Build the application as a single deployable unit with clearly organized internal modules. Ensure proper separation of concerns within the codebase using folders, packages, or layers while maintaining a unified deployment structure."
PROCESS:"
 Workflow:
    STEP-1:"Understand the complete scope of the application, including functional requirements, user roles, and business workflows."
    STEP-2:"Select or confirm a technology stack suitable for monolithic deployment.
    If specified by the user, store the stack in LOCAL_MEMORY.CACHE()
    If not specified, choose a stable, well-supported stack and store it in LOCAL_MEMORY.CACHE()"
    STEP-3:
    "Define internal layers such as:
    Presentation/UI layer
    Business logic layer
    Data access layer
    Integration/utilities layer"
    STEP-4:"Map all application features (e.g., product management, order handling, payments, offers) to internal modules within the single codebase."
    STEP-5:
    "Design a unified database schema and shared data models to be used across all modules."
    STEP-6:"Implement features incrementally, ensuring each module follows defined coding standards and integrates seamlessly with others."
    STEP-7:"Test the application as a whole, including unit tests, integration tests, and end-to-end workflows."
    STEP-8:"Package and prepare the application for deployment as a single executable or service."
ALTER:"Allow modifications to features or internal modules by updating the centralized codebase. Ensure that changes are assessed for system-wide impact before implementation."
MAINTAIN:"Maintain versioned releases of the monolithic application. Track changes centrally and ensure rollback capability in case of errors or regressions."
RULE:"Maintain clear internal modularization despite single deployment
Avoid tight coupling between unrelated components
Ensure consistent coding standards across modules
Prevent duplication of business logic
Optimize performance to avoid bottlenecks within the single application"
MANAGE:"Manage the entire application lifecycle from a single repository and deployment pipeline. Document internal modules, dependencies, and configuration settings clearly."
MONITOR:"Monitor application health, performance, logs, and errors as a single system. Establish alerts for resource usage, failures, and abnormal behavior."
PROTECT:"Implement centralized security measures including authentication, authorization, input validation, and dependency vulnerability checks to protect the entire application."
COLLABORATE:"Use AI tools, development frameworks, and automation to enhance code quality, testing coverage, and deployment reliability within the monolithic structure."
EXECUTE:"Execute the application development and deployment by strictly following the defined intent, architecture rules, workflows, and operational boundaries of the Monolithic Architecture."
