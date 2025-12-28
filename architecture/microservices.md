INTENT:
"Design and implement the application using a Microservices Architecture, where the system is composed of multiple independent, loosely coupled services. Each service is responsible for a specific business capability and can be developed, deployed, and scaled independently. This architecture is intended for large, complex, and highly scalable systems."

CREATE:
"Create an application composed of multiple autonomous microservices, each encapsulating its own business logic, data storage, and APIs. Services must communicate through well-defined synchronous or asynchronous interfaces."

BUILD:
"Build the system by developing, deploying, and managing microservices independently. Ensure service isolation, fault tolerance, scalability, and resilience using appropriate infrastructure and communication patterns."

PROCESS:
"Workflow:
    
    STEP-1:
    'Understand the complete business domain and decompose it into independent business capabilities suitable for microservices.'

    STEP-2:
    'Select or confirm a technology stack for microservices, including service frameworks, communication protocols, and infrastructure.
    If specified by the user, store the stack in LOCAL_MEMORY.CACHE()
    If not specified, choose a scalable and cloud-native stack and store it in LOCAL_MEMORY.CACHE()'

    STEP-3:
    'Define service boundaries, responsibilities, and ownership to avoid tight coupling and shared state.'

    STEP-4:
    'Design service-specific APIs and communication patterns (REST, gRPC, messaging).'

    STEP-5:
    'Design independent data stores per service to prevent cross-service data dependencies.'

    STEP-6:
    'Implement services with resilience patterns such as retries, circuit breakers, and timeouts.'

    STEP-7:
    'Test services independently and in integration, including contract testing and failure scenarios.'

    STEP-8:
    'Deploy microservices using containerization and orchestration platforms with proper configuration and scaling policies.'"

ALTER:
"Allow independent modification, scaling, or replacement of individual services without impacting the entire system, provided service contracts remain stable or versioned."

MAINTAIN:
"Maintain independent versioning for each microservice. Track service-level changes and ensure rollback capability at the service level."

RULE:
"Ensure loose coupling and high cohesion within services
Avoid shared databases across services
Maintain clear and versioned service contracts
Design for failure and resilience
Automate testing, deployment, and scaling"

MANAGE:
"Manage microservices using centralized observability, configuration management, service discovery, and documentation systems."

MONITOR:
"Monitor service health, inter-service communication, latency, error rates, and resource utilization across the distributed system."

PROTECT:
"Protect the system by enforcing service-level security, authentication, authorization, secure communication, and continuous vulnerability scanning."

COLLABORATE:
"Use AI tools, cloud-native platforms, and automation to optimize service design, deployment efficiency, and operational reliability."

EXECUTE:
"Execute the application development and deployment by strictly following the defined intent, architecture rules, workflows, and operational boundaries of the Microservices Architecture."

