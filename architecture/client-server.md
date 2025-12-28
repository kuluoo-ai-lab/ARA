INTENT:
"Design and implement the application using a Client–Server Architecture, where the client is responsible for user interaction and presentation, and the server handles business logic, data processing, authentication, and persistence. This architecture is intended for web and network-based applications that require centralized control, scalability, and distributed client access."

CREATE:
"Create an application with a clear separation between client-side and server-side components. The client application handles UI, user experience, and request initiation, while the server application manages APIs, business logic, database operations, and third-party integrations."

BUILD:
"Build the system using independent client and server components connected through secure and well-defined communication protocols such as REST or GraphQL APIs. Ensure scalability, reliability, and secure data exchange across the network."

PROCESS:
"Workflow:
    
    STEP-1:
    'Understand the complete scope of the application, including user interactions, data flows, and network communication requirements.'

    STEP-2:
    'Select or confirm suitable client-side and server-side technology stacks.
    If specified by the user, store both stacks in LOCAL_MEMORY.CACHE()
    If not specified, choose proven and compatible technologies and store them in LOCAL_MEMORY.CACHE()'

    STEP-3:
    'Define client-side responsibilities such as UI rendering, state management, user input handling, and API consumption.'

    STEP-4:
    'Define server-side responsibilities such as API design, business logic implementation, authentication, authorization, and database interaction.'

    STEP-5:
    'Design API contracts, request/response schemas, and data models for communication between client and server.'

    STEP-6:
    'Implement the client and server independently while strictly adhering to the defined API contracts.'

    STEP-7:
    'Test client–server interactions, including network latency, error handling, security validation, and data consistency.'

    STEP-8:
    'Deploy client and server components separately with proper environment configuration, networking, and access control.'"

ALTER:
"Allow independent modifications to client-side or server-side components. Ensure that any API-level changes are versioned and assessed for backward compatibility before implementation."

MAINTAIN:
"Maintain separate versioned releases for client and server applications. Track compatibility between versions and ensure rollback options are available for both components."

RULE:
"Enforce strict separation of client and server responsibilities
Do not expose sensitive logic or credentials on the client
Validate all client inputs on the server
Maintain clear and versioned API documentation
Optimize network communication and error handling"

MANAGE:
"Manage client and server codebases using separate repositories or a structured monorepo. Document APIs, environment configurations, deployment pipelines, and integration dependencies clearly."

MONITOR:
"Monitor server health, API performance, request latency, error rates, and client-side failures. Establish alerts for service degradation and communication issues."

PROTECT:
"Protect the system by enforcing secure communication (HTTPS), authentication and authorization mechanisms, rate limiting, input validation, and regular dependency vulnerability checks on both client and server."

COLLABORATE:
"Use AI tools, testing frameworks, and automation to improve client–server integration quality, reduce defects, and enhance deployment reliability."

EXECUTE:
"Execute the application development and deployment by strictly following the defined intent, architecture rules, workflows, and operational boundaries of the Client–Server Architecture."

