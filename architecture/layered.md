INTENT:"Design and implement the application using a Layered Architecture, where the system is organized into distinct layers, each with a specific responsibility. This architecture is best suited for structured, maintainable applications that require clear separation of concerns while keeping overall complexity low."
CREATE:"Create an application structured into well-defined layers such as presentation, application/service, domain/business logic, and data access layers. Each layer must interact only with its adjacent layers through clearly defined interfaces."
BUILD:"Build the application by strictly enforcing layer boundaries. Ensure that each layer is independently testable, maintainable, and replaceable without affecting unrelated layers."
PROCESS:
"Workflow:
    STEP-1:"Understand the complete application requirements and identify responsibilities that naturally map to architectural layers."
    STEP-2:"Confirm or determine the technology stack suitable for a layered design.
    If provided by the user, store it in LOCAL_MEMORY.CACHE()
    If not provided, select a stack that supports clean layering and store it in LOCAL_MEMORY.CACHE()"
    STEP-3:"Define core layers, typically including:
    Presentation Layer (UI, controllers, request handling)
    Application/Service Layer (use cases, orchestration)
    Domain/Business Layer (core business rules and logic)
    Data Access Layer (repositories, database interaction)"
    STEP-4:"Assign application features (e.g., product listing, order management, payments, offers) to the appropriate layers based on responsibility."
    STEP-5:"Define interfaces and contracts between layers to prevent tight coupling."
    STEP-6:"Implement each layer incrementally, ensuring that lower layers do not depend on higher layers."
    STEP-7:"Perform layer-specific testing (unit tests) and cross-layer integration testing."
    STEP-8:"Package and deploy the application while preserving the integrity of the layered structure."
ALTER:"Allow changes within a specific layer without impacting others, as long as layer contracts remain intact. Validate all changes for architectural compliance before applying them."
MAINTAIN:"Maintain version control at both application and layer levels. Track changes clearly and support rollback when layer-specific issues arise."
RULE:"Enforce strict separation of concerns
  Prevent direct access to non-adjacent layers
  Keep business logic isolated from UI and data layers
  Avoid duplication of logic across layers
  Maintain consistent naming and documentation per layer"
MANAGE:"Manage the application using a structured repository layout that mirrors the layered design. Document responsibilities, interfaces, and dependencies for each layer."
MONITOR:"Monitor application behavior per layer, including response times, errors, and resource usage, to quickly identify issues within specific layers."
PROTECT:"Apply security controls at appropriate layers, such as authentication in the presentation layer, authorization in the service layer, and data protection in the data access layer."
COLLABORATE:"Leverage AI tools, frameworks, and automation to validate layer boundaries, improve code quality, and ensure architectural consistency."
EXECUTE:"Execute development and deployment by strictly following the layered architecture principles, workflows, and defined constraints to deliver a structured and maintainable application."
