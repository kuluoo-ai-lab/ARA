# AGENT & AGENTIC SYNTAX DEFINITION

---

## TABLE OF CONTENTS

1. Executive Summary
2. Core Concepts
3. AGENT Syntax (Complete Formal Grammar)
4. AGENTIC Syntax (Complete Formal Grammar)
5. Semantic Actions
6. Real-World Examples
7. Best Practices
8. Implementation Guide

---

## EXECUTIVE SUMMARY

### What Are Agents and Agentic?

**AGENT:** A declarative unit defining an autonomous entity with:
- Identity (agent_name)
- Purpose (workflow/execution logic)
- Data sources (APIs, databases, files)
- Decision mechanisms (IF/THEN rules)
- Communication interface (signals, events)

**AGENTIC:** A coordination layer that:
- Orchestrates multiple agents
- Defines inter-agent communication
- Manages event triggers
- Sequences parallel/serial execution
- Handles agent lifecycle

### Key Features

| Feature | Purpose |
|---------|---------|
| **Agent Isolation** | Each agent has independent state |
| **Signal-Driven** | Agents communicate via signals/events |
| **Workflow Definition** | Multi-step processes with conditions |
| **State Management** | Persistent memory and cache |
| **Error Handling** | Built-in fault tolerance |
| **Monitoring** | Real-time activity tracking |

---

## CORE CONCEPTS

### Agents as Autonomous Units

An AGENT is defined as:
- Independent execution unit
- With isolated state
- With workflow-driven logic
- With signal-based communication
- With error handling capabilities
- With persistent memory (CACHE)

### Signal System

Signals are the primary communication mechanism:
- Equality signals: `agent.signal == "value"`
- Threshold signals: `agent.value > 30`
- State signals: `agent.status = "ready"`
- Event signals: `agent.event_fired = true`

Broadcasting scopes:
- LOCAL: Only to parent agent
- GLOBAL: To all agents in system
- GROUP: To specific agent group
- DIRECT: To named agent(s)

### Workflow Structure

WORKFLOW defines step-by-step logic:
- Sequential steps (STEP-1, STEP-2, ...)
- Conditional execution (IF/THEN)
- Loops and iteration
- Signal checking/setting
- Data transformation
- External calls (APIs, databases)

### Multi-Agent Orchestration

AGENTIC layer manages:
- Agent dependencies
- Execution order
- Signal routing
- Parallel execution groups
- Error handling and recovery
- Resource management

---

## AGENT FORMAL SYNTAX

### BNF Grammar Definition

```
AGENT_BLOCK ::=
    "<agent" AGENT_ID ">"
        AGENT_DECLARATION
        AGENT_PROPERTIES
        AGENT_MECHANISMS
    "</agent>"

AGENT_DECLARATION ::=
    "agent_name" "=" STRING
    | "agent_id" "=" IDENTIFIER

AGENT_PROPERTIES ::=
    PROPERTY*

PROPERTY ::=
    PROPERTY_KEY "=" PROPERTY_VALUE

AGENT_MECHANISMS ::=
    WORKFLOW
    | DECISION
    | SIGNAL_DEFINITION
    | STATE_DEFINITION

WORKFLOW ::=
    "WORKFLOW" ":"
        STEP*

STEP ::=
    "STEP-" NUMBER ":" STEP_ACTION
    | "STEP-" NUMBER ":" "IF" CONDITION "THEN" STEP_ACTION

DECISION ::=
    "DECISION" ":"
        CONDITION ":" THEN_ACTION
```

### User-Friendly AGENT Syntax

```
<agent>
    agent_name = "AgentName"
    data_source = "API:source"
    environment = "context"
    role = "What agent does"
    timeout = 30
    retry_count = 3
    priority = 8
    state_mode = "STATEFUL"
    
    WORKFLOW:
        STEP-1: RECEIVE data FROM source
        STEP-2: PROCESS data
        STEP-3: STORE result
        STEP-4: EMIT signal="done"
    
    DECISION:
        IF condition THEN SET signal
    
    SIGNAL:
        - signal_name: "name"
          signal_type: "THRESHOLD"
          trigger_condition: condition
          broadcast_scope: "GLOBAL"
    
    CACHE:
        - variable_name

</agent>
```

---

## AGENTIC FORMAL SYNTAX

### BNF Grammar Definition

```
AGENTIC_BLOCK ::=
    "<agentic>"
        ORCHESTRATION_RULES
    "</agentic>"

ORCHESTRATION_RULES ::=
    TRIGGER_RULE*

TRIGGER_RULE ::=
    "START" ["WHEN" CONDITION]
    ACTION_SEQUENCE
    ["PARALLEL" action_group]
    ["SERIAL" action_group]

ACTION ::=
    agent_name "(" parameters ")"
    | "WAIT" DURATION
    | "RETRY" INTEGER "times"
    | "FALLBACK" action_name
```

### User-Friendly AGENTIC Syntax

```
<agentic>
    START WHEN condition
    agent1() → agent2() → agent3()
    
    # Or with error handling
    TRY {
        critical_agent.execute()
    } RETRY 3 times CATCH error {
        recovery_agent.handle(error)
    }
    
    # Or parallel execution
    PARALLEL {
        agent1.task() |
        agent2.task() |
        agent3.task()
    }
</agentic>
```

---

## SEMANTIC ACTIONS (FOR CODE GENERATION)

### INTENT: Understand Requirement
Parse user input, identify project type, decide tech stack, store in cache.

### CREATE: Plan Code Generation
Retrieve language rules, list requirements as checklist, create roadmap.

### BUILD: Generate Production Code
Execute plan, implement features, add error handling, security, tests.

### ALTER: Modify Code
Accept modifications, ask clarifying questions, make surgical changes.

### PROTECT: Security Hardening
Scan dependencies, check vulnerabilities, remove unsafe packages.

### RULE: Quality Verification
Lint code, verify security, scan for vulnerabilities, run tests.

### MAINTAIN: Version Control
Name versions, log changes, allow version switching, document reasoning.

### MANAGE: Version History
Track changes, show change summary, allow version comparison.

### COLLABORATE: Multi-AI Collaboration
Engage multiple AI models, combine strengths, verify consistency.

### EXECUTE: Execute All Objectives
Remember all objectives, execute with all in mind, verify each.

### MONITOR: Track Activities
Set boundaries, track activities, alert on issues, log everything.

---

## REAL-WORLD EXAMPLES

### Example 1: Weather Classification Agent

```
<agent1>
    agent_name = "Weather Agent"
    data_source = "API:openweather"
    role = "Collect and classify weather data"
    timeout = 30
    retry_count = 3
    
    WORKFLOW:
        STEP-1: RECEIVE weather_data FROM api
        STEP-2: VALIDATE weather_data
        STEP-3: CLASSIFY temperature
                WHERE: HOT >= 30, OKAY 21-29, COLD <= 20
        STEP-4: STORE classification TO database
        STEP-5: EMIT signal="weather_classified"
    
    DECISION:
        IF temperature >= 30 THEN SET signal.hot = true
        IF temperature <= 20 THEN SET signal.cold = true
    
    SIGNAL:
        - signal_name: "temperature_hot"
          signal_type: "THRESHOLD"
          trigger_condition: temperature >= 30
          broadcast_scope: "GLOBAL"
</agent1>
```

### Example 2: Booking Orchestration

```
<agentic>
    START WHEN weather_agent.signal == "temperature_hot"
    
    EXECUTE booking_agent({
        property_type: "beach_house",
        check_in: today(),
        check_out: today() + 3
    })
    
    THEN payment_agent({
        booking_id: booking_agent.last_booking_id,
        payment_method: "card"
    })
    
    THEN notification_agent({
        message: "Booking confirmed!",
        recipient: current_user
    })
</agentic>
```

---

## BEST PRACTICES

### 1. Agent Naming
✅ GOOD: weather_data_collector, booking_processor
❌ BAD: agent1, WeatherAgent123

### 2. Signal Naming
✅ GOOD: temperature_hot, booking_ready, data_processed
❌ BAD: signal1, s, X

### 3. Workflow Clarity
✅ GOOD: Clear, descriptive step names
❌ BAD: do stuff, more stuff, finish

### 4. Error Handling
✅ GOOD: TRY-CATCH with fallback
❌ BAD: Just execute and hope

### 5. Signal Scope
✅ GOOD: Specific scopes (GROUP, DIRECT)
❌ BAD: Everything GLOBAL

---

## IMPLEMENTATION CHECKLIST

### AGENT Implementation
- ☐ Agent declaration with name and ID
- ☐ Data source configuration
- ☐ Role description
- ☐ Workflow with all steps
- ☐ Decision logic
- ☐ Signal definitions
- ☐ State management (CACHE)
- ☐ Error handling

### AGENTIC Implementation
- ☐ START trigger conditions
- ☐ Action sequences
- ☐ Parallel execution groups
- ☐ Error handling with retry
- ☐ Wait operations with timeout
- ☐ Conditional branching
- ☐ Logging and monitoring

---

📊 THE 12 ARA KEYWORD CATEGORIES
Category	Keywords	Purpose	Maps To
1. INTENT	61 kw	Declare WHY	Agent purpose, decision making
2. RULE/REGULATE	60 kw	Define WHAT'S ALLOWED	Access control, constraints
3. PROCESS	65 kw	Plan HOW	Workflow planning, sequences
4. EXECUTE	65 kw	Do IT	Run operations, state changes
5. COLLABORATE	65 kw	Coordinate WITH OTHERS	Inter-agent communication
6. MONITOR	65 kw	Observe WHAT HAPPENED	Tracking, observation
7. PROTECT	65 kw	Enforce CONSTRAINTS	Security, validation
8. MANAGE	65 kw	Control OPTIMIZE	System management
9. ALTER/EDIT	65 kw	Transform STATE	Data modification
10. MAINTAIN	65 kw	Keep CONSISTENT	Consistency, lifecycle
11. CREATE	50 kw	Make NEW	Creation, generation
12. BUILD	22 kw	Construct COMPONENTS	Assembly, construction
🔗 INTEGRATION MAP
How ARA Keywords Map to Systems
text
ARA Categories
    ↓
INTENT (61 kw)           → AGENT declaration + PURPOSE
RULE/REGULATE (60 kw)    → DATA validation + SIGNAL rules
PROCESS (65 kw)          → WORKFLOW steps + sequencing
EXECUTE (65 kw)          → WORKFLOW actions + operations
COLLABORATE (65 kw)      → AGENTIC communication + signals
MONITOR (65 kw)          → WORKFLOW observation + tracking
PROTECT (65 kw)          → DATA encryption + validation
MANAGE (65 kw)           → AGENT lifecycle + orchestration
ALTER/EDIT (65 kw)       → DATA transformation + operations
MAINTAIN (65 kw)         → DATA persistence + consistency
CREATE (50 kw)           → INTENT-CREATE-BUILD phase
BUILD (22 kw)            → INTENT-CREATE-BUILD phase
    ↓
AGENT + AGENTIC + DATA Systems
📝 INTEGRATED AGENT SYNTAX (Using ARA Keywords)
Complete AGENT Block with ARA Keywords
text
<agent>
    # INTENT Keywords (1-61): Declare purpose & goals
    agent_name = "WeatherCollector"
    purpose: STRING = "Collect and classify weather data"
    task: STRING = "Fetch weather from API"
    intent: STRING = "Provide real-time weather updates"
    objective: STRING = "Temperature classification"
    
    # RULE/REGULATE Keywords (62-121): Define constraints
    timeout = 30
    retry_count = 3
    priority = 8
    access: STRING = "GATEKEEPER:api_access"
    constraint: STRING = "rate_limit:100_per_minute"
    
    # PROCESS Keywords (122-186): Plan workflow
    workflow_strategy: STRING = "sequential"
    
    WORKFLOW:
        # PROCESS: PLAN (122-129)
        STEP-1: PLAN data collection strategy
                OBTAIN weather_data FROM api
                REASON about data quality
        
        # PROCESS: SEQUENCE (130-139)
        STEP-2: ACTIVATE classification logic
                STEP 1..N process each reading
                INITIAL validation
                MIDDLE aggregation
                FINAL decision
        
        # PROCESS: OPTIMIZE (140-145)
        STEP-3: OPTIMIZE performance
                COMPARE different approaches
                ADAPT to conditions
                TRADEOFF accuracy vs speed
        
        # EXECUTE Keywords (187-251): Do operations
        STEP-4: GENERATE classification
                CHANGE temperature to celsius
                CONTAIN result in object
                PRODUCE output structure
        
        # COLLABORATE Keywords (252-316): Inter-agent signals
        STEP-5: EMIT signal="weather_classified"
                BROADCAST scope="GLOBAL"
                SEND to booking_agent
        
        # MONITOR Keywords (317-381): Track activity
        STEP-6: MONITOR execution
                TRACK classification accuracy
                MEASURE temperature variance
                REPORT to dashboard
    
    # PROTECT Keywords (382-446): Security & validation
    DECISION:
        # RULE: Apply constraints
        IF temperature >= 30 THEN
            SET signal.hot = true
            VERIFY against SCHEMA
            VALIDATE temperature_range
        
        # ALTER/EDIT Keywords (512-576): Data transformation
        TRANSFORM temperature TO readable_format
        CONVERT celsius TO fahrenheit
        PREPARE for storage
    
    # SIGNAL: Using MONITOR & COLLABORATE keywords
    SIGNAL:
        - signal_name: "temperature_high"
          signal_type: "THRESHOLD"
          trigger_condition: temperature > 30
          broadcast_scope: "GLOBAL"
          pattern: "MONITOR.TRACK"
    
    # MAINTAIN Keywords (577-641): Keep consistent
    CACHE:
        - last_reading
        - classification_cache
        - timestamp

</agent>
🔄 INTEGRATED AGENTIC SYNTAX (Using ARA Keywords)
Multi-Agent Orchestration with ARA Keywords
text
<agentic>
    # INTENT: Declare purpose (1-61)
    purpose: "Weather-based hotel booking system"
    
    # PROCESS: Plan workflow (122-186)
    workflow_strategy: "sequential"
    
    # RULE: Define constraints (62-121)
    constraints: [
        "rate_limit:100_per_minute",
        "timeout:30",
        "priority:high"
    ]
    
    # EXECUTE: Main orchestration (187-251)
    START WHEN user.location_ready
    
    # PROCESS: Sequence operations (130-139)
    STEP 1: weather_agent.collect()
            ACTIVATE data gathering
            INITIAL validation
            REASON about quality
    
    STEP 2: weather_agent.classify()
            COMPARE temperatures
            OPTIMIZE classification
            PRODUCE results
    
    # COLLABORATE: Inter-agent communication (252-316)
    THEN booking_agent.process({
        location: weather_agent.location,
        temperature: weather_agent.temperature,
        classification: weather_agent.classification
    })
    
    # EXECUTE: State changes (187-251)
    booking_agent CHANGE status TO "processing"
    
    # MONITOR: Track activity (317-381)
    MONITOR booking_agent.progress
    TRACK booking_status
    MEASURE response_time
    
    # PROTECT: Enforce security (382-446)
    VERIFY booking_data AGAINST schema
    VALIDATE payment_info
    AUTHENTICATE user
    
    # MAINTAIN: Keep consistent (577-641)
    THEN notification_agent.send({
        user: current_user,
        hotel: booking_agent.result.hotel,
        status: "confirmed"
    })
    
    # CREATE/BUILD: Generate results (642-713)
    OUTPUT: booking_confirmation
    DOCUMENT: transaction_record

</agentic>
💾 INTEGRATED DATA SYNTAX (Using ARA Keywords)
Data Blocks with ARA Keywords
text
<data>
    # INTENT: Define purpose (1-61)
    <data_config>
        # INTENT: PURPOSE, TASK, OBJECTIVE
        purpose: STRING = "Application configuration"
        task: STRING = "Store API credentials"
        
        # RULE: Define constraints (62-121)
        constraint: STRING = "encrypted"
        access: STRING = "gatekeeper_required"
        legal: BOOL = true
        
        # PROTECT: Security keywords (382-446)
        api_key: STRING = "sk-encrypted-key"
        encrypted: BOOL = true
        authenticate: BOOL = true
        
        # MANAGE: System control (447-511)
        automate: BOOL = true
        install: STRING = "production"
        license: STRING = "commercial"
        
        <api_endpoints>
            # CREATE: Making new (642-691)
            chat_completion: STRING = "/chat/completions"
            embeddings: STRING = "/embeddings"
            models: STRING = "/models"
        </api_endpoints>
    </data_config>
    
    # MAINTAIN: Keep consistent (577-641)
    <data_user_profile>
        # INTENT: What this data is for
        user_id: STRING = "user_12345"
        email: STRING = "user@example.com"
        
        # EXECUTE: Current state (187-251)
        status: STRING = "active"
        is_verified: BOOL = true
        
        # PROCESS: How to process (122-186)
        preferences: OBJECT = {
            # PROCESS keywords
            strategy: "optimize_performance",
            approach: "parallel_execution",
            theme: "dark"
        }
        
        # ALTER/EDIT: Transform data (512-576)
        <editable_preferences>
            theme: STRING = "dark"
            language: STRING = "en"
            notifications: BOOL = true
        </editable_preferences>
        
        # MONITOR: Track activity (317-381)
        last_login: INT = 1735558500
        login_count: INT = 42
        activity_score: INT = 95
    </data_user_profile>
    
    # COLLABORATE: Inter-system communication (252-316)
    <data_shared_state>
        # COLLABORATE: Work together
        shared_session_token: STRING = "sess_abc123"
        participant_ids: ARRAY = ["agent1", "agent2", "agent3"]
    </data_shared_state>

</data>
🎯 INTENT-CREATE-BUILD WITH ARA KEYWORDS
Complete Pipeline Using 713 Keywords
text
PHASE 1: INTENT (Declare WHY - Keywords 1-61)
───────────────────────────────────────────
STEP-1: TASK - Understand work unit
        INTENT - Identify expressed purpose
        PURPOSE - Understand reason
        OBJECTIVE - Set specific goal
        REASON - Justify requirement
        THINK - Cognitive analysis
        DECIDE - Make choice

STEP-2: DECISION FRAMING (Keywords 7-12)
        LOGIC - Apply formal reasoning
        STRATEGY - Plan approach
        STYLE - Manner of execution

PHASE 2: CREATE (Plan Structure - Keywords 122-186)
──────────────────────────────────────────────
STEP-3: PLAN (Keywords 122-129)
        PLAN - Create scheme
        OPTIONS - Available choices
        KNOWLEDGE - Accumulated info
        STRATEGY - Long-term approach
        IMAGINE - Conceive mentally
        LENS - Interpretive framework

STEP-4: SEQUENCE (Keywords 130-139)
        STEP 1..N - Numbered progression
        INITIAL - First stage
        MIDDLE - Middle stage
        FINAL - Last stage
        ACTIVATE - Turn on
        INTRODUCE - Present first time

PHASE 3: BUILD (Generate Code - Keywords 692-713)
──────────────────────────────────────────────
STEP-5: BUILD (Keywords 692-704)
        BUILD - Construct assembly
        DIVIDE - Separate into parts
        DUPLICATE - Make exact copy
        DRAW - Create picture
        DRIVE - Propel forward
        DRILL - Practice

STEP-6: CREATE (Keywords 642-691)
        CREATE - Make new
        DISCOVER - Find or learn
        DECIDE - Make decision
        DECLARE - Announce formally
        DISTRIBUTE - Spread or dispense
        DIVERSITY - Variety or multiplicity

SEMANTIC ACTIONS (All 713 Keywords):
────────────────────────────────────
ALTER (512-576):        IMPORT, EXPORT, TRANSFORM, CONVERT
PROTECT (382-446):      AUTHENTICATE, VERIFY, VALIDATE, ENCRYPT
RULE (62-121):          CONSTRAINT, LIMIT, ACCESS, APPROVE
MAINTAIN (577-641):     CONSISTENCY, TRANSACTION, LIFECYCLE, EXPIRE
MANAGE (447-511):       AUTOMATE, INSTALL, LICENSE, ORCHESTRATE
COLLABORATE (252-316):  SEND, RECEIVE, MATCH, BROADCAST
EXECUTE (187-251):      GENERATE, CHANGE, ORDER, EXCHANGE
MONITOR (317-381):      TRACK, MEASURE, REPORT, ANALYZE

📋 KEYWORD REFERENCE BY SYSTEM
AGENT Keywords
INTENT (1-61): PURPOSE, TASK, OBJECTIVE, START, END, ERROR, RESULT, MEMORY.SAVE
RULE (62-121): CONSTRAINT, LIMIT, ACCESS, APPROVE, SEQUENCE, STANDARD
PROCESS (122-186): PLAN, STEP, SEQUENCE, OPTIMIZE, ITERATE, PROBLEM, SOLUTION
EXECUTE (187-251): GENERATE, CHANGE, ORDER, EXCHANGE, LOCK, UNLOCK

AGENTIC Keywords
COLLABORATE (252-316): SEND, RECEIVE, MATCH, IF, EQUAL, DATA, PUSH, PULL
MONITOR (317-381): TRACK, MEASURE, REPORT, ANALYZE, IDENTIFY, TAG
PROTECT (382-446): VERIFY, VALIDATE, AUTHENTICATE, THREAT, BLOCK, ALLOW
MANAGE (447-511): ASSIGN, RESOURCE, AUTOMATE, INSTALL, RETIRE, LICENSE

DATA Keywords
ALTER/EDIT (512-576): IMPORT, EXPORT, TRANSFORM, CONVERT, MODEL, PREPARE
MAINTAIN (577-641): COMPLIANCE, CONSISTENCY, TRANSACTION, LIFECYCLE, EXPIRE
CREATE (642-691): PROTOTYPE, DESIGN, VISUALIZE, DISCOVER, DISTRIBUTE
BUILD (692-713): BUILD, DIVIDE, DUPLICATE, DOCUMENT, DOWNLOAD

✅ COMPLETE EXAMPLE: Weather Booking System
text
<data>
    <data_weather_config>
        # INTENT keywords
        purpose: STRING = "Weather data storage"
        # PROTECT keywords
        encrypted: BOOL = true
        # MAINTAIN keywords
        consistency: BOOL = true
        # CREATE keywords
        created_at: STRING = "2025-12-30"
    </data_weather_config>
</data>

<agent1>
    agent_name = "WeatherAgent"
    # INTENT keywords
    purpose = "Collect weather data"
    task = "Fetch from API"
    objective = "Classify temperature"
    
    # RULE keywords
    timeout = 30
    constraint = "rate_limit"
    limit = 100
    access = "api_required"
    
    # PROCESS keywords
    strategy = "sequential"
    
    WORKFLOW:
        # PROCESS keywords: PLAN, STEP, SEQUENCE
        STEP-1: PLAN weather collection
        STEP-2: STEP 1..N iterate readings
        STEP-3: OPTIMIZE for performance
        
        # EXECUTE keywords: GENERATE, CHANGE, PRODUCE
        STEP-4: GENERATE classification
        STEP-5: CHANGE format to JSON
        STEP-6: PRODUCE output
        
        # COLLABORATE keywords: EMIT signal
        STEP-7: EMIT signal="classified"
    
    SIGNAL:
        - signal_name: "temperature_high"
          # MONITOR keywords: TRACK
          # PROTECT keywords: VERIFY
          trigger_condition: temperature > 30
</agent1>

<agent2>
    agent_name = "BookingAgent"
    # INTENT keywords
    purpose = "Process hotel booking"
    
    WORKFLOW:
        # COLLABORATE keywords: RECEIVE signal
        STEP-1: RECEIVE signal FROM weather_agent
        
        # PROCESS keywords: PLAN, OPTIMIZE
        STEP-2: PLAN booking strategy
        STEP-3: OPTIMIZE cost
        
        # ALTER/EDIT keywords: TRANSFORM
        STEP-4: TRANSFORM location TO hotel_id
        
        # PROTECT keywords: VALIDATE, AUTHENTICATE
        STEP-5: VALIDATE booking_data
        STEP-6: AUTHENTICATE user
        
        # MAINTAIN keywords: CONSISTENCY
        STEP-7: MAINTAIN data consistency
        
        # CREATE keywords: DECLARE
        STEP-8: DECLARE booking_complete
</agent2>

<agentic>
    # INTENT keywords: PURPOSE, OBJECTIVE
    purpose = "Book hotel based on weather"
    objective = "Complete booking by evening"
    
    # PROCESS keywords: PLAN, SEQUENCE
    PLAN: sequential execution
    SEQUENCE: weather → booking → notification
    
    # EXECUTE keywords
    START WHEN user.ready
    
    # COLLABORATE keywords: SEND, RECEIVE
    weather_agent.collect()
        → booking_agent.process()
        → notification_agent.send()
    
    # MONITOR keywords: TRACK, MEASURE
    MONITOR: weather_agent.status
    TRACK: booking_progress
    MEASURE: response_time
    
    # PROTECT keywords: VERIFY
    VERIFY: all data valid
    
    # MAINTAIN keywords: CONSISTENCY
    MAINTAIN: transaction consistency
    
    # CREATE/BUILD keywords: DECLARE, BUILD
    DECLARE: booking_confirmation
    BUILD: transaction_record

</agentic>

AT A GLANCE
AGENT Structure
text
<agent>
    agent_name = "AgentName"
    data_source = "SOURCE"
    role = "DESCRIPTION"
    
    WORKFLOW:
        STEP-1: ACTION
        STEP-2: IF condition THEN action
        STEP-3: MORE STEPS
    
    DECISION:
        IF condition THEN SET signal
    
    SIGNAL:
        - signal_name: "name"
          trigger_condition: condition
          broadcast_scope: "GLOBAL"
</agent>
AGENTIC Structure
text
<agentic>
    START WHEN condition
    agent1() → agent2() → agent3()
    
    # or
    
    START WHEN condition
    PARALLEL {
        agent1() |
        agent2() |
        agent3()
    }
</agentic>
QUICK SYNTAX GUIDE
Agent Declarations
text
agent_name = "Name"                    # REQUIRED
agent_id = "agent_001"                 # OPTIONAL
data_source = "API:name"               # OPTIONAL
environment = "www.example.com"        # OPTIONAL
role = "What agent does"               # REQUIRED
timeout = 30                           # OPTIONAL (seconds)
retry_count = 3                        # OPTIONAL
priority = 8                           # OPTIONAL (1-10)
state_mode = "STATEFUL"                # OPTIONAL
Workflow Actions
text
RECEIVE data FROM source               # Get data
SEND data TO destination               # Send data
STORE data TO database                 # Save to DB
RETRIEVE data FROM storage             # Load from DB
PROCESS data APPLY rules               # Transform
TRANSFORM data TO format               # Change format
VALIDATE data AGAINST schema           # Check format
ANALYZE data FOR insights              # Examine
CLASSIFY data INTO categories          # Categorize
CACHE data IN memory                   # Store in cache
EMIT signal = "name"                   # Send signal
SET variable = value                   # Assign value
Step Types
text
STEP-N: ACTION                         # Simple action
STEP-N: IF condition THEN action       # Conditional
STEP-N: LOOP WHILE condition DO action # Loop
STEP-N: PARALLEL { a | b | c }         # Parallel
STEP-N: TRANSACTION { a; b; COMMIT }   # Atomic
Decision Syntax
text
DECISION:
    IF condition THEN action
    IF condition2 THEN action2
    ELSE default_action
Signal Definition
text
SIGNAL:
    - signal_name: "name"
      signal_type: "THRESHOLD"         # or EVENT, STATE, EQUALITY
      trigger_condition: condition
      broadcast_scope: "GLOBAL"        # or LOCAL, GROUP, DIRECT
Agentic Triggers
text
START WHEN condition                   # Start when true
START AFTER duration                   # Start after time
START WITH PRIORITY n                  # Set priority

agent1() → agent2() → agent3()         # Sequential
PARALLEL { a | b | c }                 # Parallel
IF condition THEN action ELSE fallback # Conditional
TRY action RETRY n CATCH error         # Error handling
WAIT_FOR signal TIMEOUT duration       # Wait for signal
WORKFLOW PATTERNS
Pattern 1: Simple Sequential
text
WORKFLOW:
    STEP-1: RECEIVE data FROM api
    STEP-2: PROCESS data
    STEP-3: STORE result
    STEP-4: EMIT signal="complete"
Pattern 2: Conditional Processing
text
WORKFLOW:
    STEP-1: RECEIVE data
    STEP-2: VALIDATE data
    STEP-3: IF valid THEN
            PROCESS data
            ELSE LOG error AND SKIP
    STEP-4: STORE result
Pattern 3: Parallel Operations
text
WORKFLOW:
    STEP-1: PARALLEL {
        VALIDATE input |
        CHECK cache |
        PREPARE database
    }
    STEP-2: PROCESS all_data
Pattern 4: Retry Loop
text
WORKFLOW:
    STEP-1: LOOP WHILE attempts < 3 DO
            CALL external_api
            IF success THEN BREAK
            ELSE WAIT 1 second AND RETRY
Pattern 5: Error Recovery
text
WORKFLOW:
    STEP-1: TRY {
            EXECUTE critical_operation()
        } CATCH error {
            EXECUTE recovery_operation()
            NOTIFY admin
        }
SIGNAL PATTERNS
Pattern 1: Threshold Signal
text
SIGNAL:
    - signal_name: "temperature_alert"
      signal_type: "THRESHOLD"
      trigger_condition: temperature > 35
      broadcast_scope: "GLOBAL"
Pattern 2: Event Signal
text
SIGNAL:
    - signal_name: "process_complete"
      signal_type: "EVENT"
      trigger_condition: STEP-5 COMPLETE
      broadcast_scope: "GROUP:processors"
Pattern 3: State Signal
text
SIGNAL:
    - signal_name: "agent_ready"
      signal_type: "STATE"
      trigger_condition: agent_state == "ready"
      broadcast_scope: "LOCAL"
AGENTIC PATTERNS
Pattern 1: Sequential Agents
text
<agentic>
    START WHEN trigger_condition
    
    agent1.collect() 
        → agent2.validate() 
        → agent3.process() 
        → agent4.store()
</agentic>
Pattern 2: Parallel Agents
text
<agentic>
    START WHEN ready
    
    PARALLEL {
        agent1.task() |
        agent2.task() |
        agent3.task()
    }
    
    THEN agent4.combine_results()
</agentic>
Pattern 3: Conditional Flow
text
<agentic>
    START WHEN agent1.complete
    
    IF agent1.result.valid THEN {
        agent2.process(agent1.result)
    } ELSE {
        agent3.handle_error(agent1.error)
    }
</agentic>
Pattern 4: Error Handling
text
<agentic>
    START WHEN booking.initiated
    
    TRY {
        payment_agent.charge()
    } RETRY 2 times CATCH error {
        booking_agent.cancel()
        user_agent.notify_error()
    }
</agentic>
Pattern 5: Wait & Timeout
text
<agentic>
    START WHEN user_action
    
    WAIT_FOR payment_confirmation 
    TIMEOUT 300 seconds
    ELSE booking_agent.refund()
</agentic>
REAL-WORLD EXAMPLES
Weather Bot
text
<agent1>
    agent_name = "Weather Bot"
    data_source = "API:weather_service"
    role = "Fetch and classify weather"
    
    WORKFLOW:
        STEP-1: RECEIVE weather_data FROM api
        STEP-2: CLASSIFY temperature HOT|COLD|OKAY
        STEP-3: STORE classification
        STEP-4: EMIT signal="classified"
    
    DECISION:
        IF temp >= 30 THEN SET signal.hot = true
        IF temp <= 20 THEN SET signal.cold = true
    
    SIGNAL:
        - signal_name: "hot"
          trigger_condition: temperature >= 30
          broadcast_scope: "GLOBAL"
</agent1>

<agentic>
    START WHEN weather_bot.hot
    booking_agent.book_beach_hotel()
</agentic>
E-Commerce Order
text
<agent1>
    agent_name = "Order Processor"
    data_source = "DATABASE:orders"
    role = "Process orders"
    
    WORKFLOW:
        STEP-1: RECEIVE order
        STEP-2: VALIDATE payment
        STEP-3: RESERVE inventory
        STEP-4: EMIT signal="ready_for_shipment"
</agent1>

<agent2>
    agent_name = "Shipment Agent"
    data_source = "DATABASE:orders"
    role = "Ship orders"
    
    WORKFLOW:
        STEP-1: WAIT_FOR order_processor.ready_for_shipment
        STEP-2: GENERATE shipping_label
        STEP-3: UPDATE tracking_info
        STEP-4: NOTIFY customer
</agent2>

<agentic>
    START WHEN user.places_order
    order_processor.process() 
        → shipment_agent.ship() 
        → customer_agent.notify()
</agentic>
COMMON MISTAKES
❌ Mistake 1: Ambiguous Signal
text
BAD:
SIGNAL:
    - signal_name: "signal"
      trigger_condition: x

GOOD:
SIGNAL:
    - signal_name: "temperature_high"
      trigger_condition: temperature > 35
❌ Mistake 2: No Timeout
text
BAD:
WAIT_FOR external_response

GOOD:
WAIT_FOR external_response TIMEOUT 30 seconds ELSE fallback()
❌ Mistake 3: Missing Error Handling
text
BAD:
payment_agent.charge(amount)

GOOD:
TRY {
    payment_agent.charge(amount)
} CATCH error {
    booking_agent.cancel()
}
❌ Mistake 4: Circular Signals
text
BAD:
Agent A emits signal → Agent B emits signal → Agent A (infinite loop)

GOOD:
Clear signal flow: A → B → C (no cycles)
❌ Mistake 5: Too Broad Broadcast
text
BAD:
SIGNAL broadcast_scope: "GLOBAL" (for every signal)

GOOD:
SIGNAL broadcast_scope: "GROUP:relevant_agents"
CHEAT SHEET
Create a Simple Agent
text
<agent>
    agent_name = "MyAgent"
    WORKFLOW:
        STEP-1: action
</agent>
Simple Workflow
text
STEP-1: RECEIVE
STEP-2: PROCESS
STEP-3: STORE
STEP-4: EMIT signal
Make a Signal
text
SIGNAL:
    - signal_name: "done"
      trigger_condition: status == "complete"
      broadcast_scope: "GLOBAL"
Listen to Signal
text
START WHEN agent.signal == "value"
next_agent.execute()
Parallel Agents
text
PARALLEL {
    agent1() |
    agent2() |
    agent3()
}
Error Handling
text
TRY { action } CATCH error { handle_error() }
Retry
text
RETRY 3 times { attempt_action() }
Wait
text
WAIT_FOR condition TIMEOUT 30 seconds ELSE fallback()
KEY CONCEPTS SUMMARY
Concept	Purpose	Example
Agent	Autonomous unit	Weather collector
Signal	Inter-agent communication	temp_hot
Workflow	Sequential steps	STEP-1, STEP-2, ...
Decision	Conditional logic	IF temp > 30 THEN ...
Agentic	Multi-agent orchestration	START WHEN ...
CACHE	Temporary memory	CACHE.SET("key", val)
RETRY	Error recovery	RETRY 3 times
PARALLEL	Concurrent execution	PARALLEL { a | b }
TIMEOUT	Time limit	TIMEOUT 30 seconds
TRY-CATCH	Exception handling	TRY { } CATCH { }
NEXT STEPS
Define your agents - What autonomous units do you need?

Plan workflows - What steps should each agent follow?

Define signals - How should agents communicate?

Create agentic rules - How should agents coordinate?

Test interactions - Verify signals flow correctly

Handle errors - Add retry and fallback logic

Monitor execution - Track performance and issues
