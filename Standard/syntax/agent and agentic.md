# AGENT & AGENTIC SYNTAX SPECIFICATION 


---

## OVERVIEW

This AGENT and AGENTIC syntax uses **prompting-based declarations** where developers describe agent behavior through structured keyword declarations.

### Core Principle
**"Declare agent INTENT, define available resources, specify processes, and govern execution with explicit checkpoints and memory."**

---

## AGENT SYNTAX

### Complete Agent Structure

```
<agent>
    TOKEN_LIMIT = maximum_tokens
    TOKEN_MIN = minimum_tokens
    TOKEN_MAX = maximum_tokens_per_execution
    
    agent_name = unique_agent_identifier
    
    environment = deployment_environment
    
    <data>
        // Data sources agent can access
    </data>
    
    intent = agent_goal_and_purpose
    
    variable = variable_declarations_and_definitions
    
    function = custom_logic_and_operations
    
    create = what_agent_generates_or_creates
    
    build = how_agent_composes_components
    
    process = reasoning_and_decision_logic
    
    alter = transformations_and_mutations
    
    manage = resource_allocation_and_lifecycle
    
    monitor = observability_and_metrics
    
    execute = actions_the_agent_takes
    
    protect = security_and_access_controls
    
    maintain = memory_caching_and_state
    
    collaborate = coordination_with_other_agents
    
    rule = constraints_and_limits
    
    checkpoint = validation_and_verification_points
    
</agent>
```

### Minimal Agent

```
<agent>
    TOKEN_LIMIT = 20000
    
    agent_name = WeatherClassifier
    
    environment = production
    
    intent = Classify live weather conditions
    
    process = Analyze temperature, humidity, wind
    
    execute = Store classifications by tag
    
    checkpoint = Verify classification accuracy
</agent>
```

---

## AGENT KEYWORDS

### 1. TOKEN_LIMIT
**Purpose:** Maximum tokens this agent can use per execution cycle

```
TOKEN_LIMIT = 20000        // Maximum tokens for agent
TOKEN_LIMIT = 50000        // For complex agents
TOKEN_LIMIT = 100000       // For heavy-duty agents
```

**Rules:**
- Set based on expected complexity
- Higher = more capable but slower
- Consider cost implications

---

### 2. TOKEN_MIN & TOKEN_MAX
**Purpose:** Minimum and maximum token boundaries

```
TOKEN_MIN = 5000           // Minimum tokens needed for safe operation
TOKEN_MAX = 25000          // Hard limit on token usage
```

**Examples:**
```
<agent>
    TOKEN_LIMIT = 20000
    TOKEN_MIN = 5000
    TOKEN_MAX = 25000
</agent>
```

---

### 3. agent_name
**Purpose:** Unique identifier for the agent

```
agent_name = DonorMatcher
agent_name = WeatherAnalyzer
agent_name = TravelOptimizer
agent_name = BookingExecutor
```

**Rules:**
- Unique within application
- CamelCase naming
- Descriptive of purpose

---

### 4. environment
**Purpose:** Deployment environment for agent

```
environment = production
environment = staging
environment = development
environment = testing
environment = cloud
environment = local
```

**Examples:**
```
<agent>
    agent_name = DonorMatcher
    environment = production
</agent>
```

---

### 5. <data>
**Purpose:** Data sources agent can access

```
<data>
    data_name = donors
    data_name = requests
    data_name = user_location
</data>
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    <data>
        data_name = donors
        connect = database
        
        data_name = blood_requests
        connect = api
        
        data_name = user_location
        connect = session
    </data>
</agent>
```

---

### 6. intent
**Purpose:** What the agent is trying to achieve (goal statement)

```
intent = Match blood donors with urgent requests
intent = Analyze weather patterns and predict conditions
intent = Optimize travel options by user preferences
intent = Execute booking transactions securely
```

**Rules:**
- Clear, single statement
- Measurable and achievable
- Guards all agent decisions

---

### 7. variable
**Purpose:** Declare variables agent uses during execution

```
variable = donor_list: Array[Donor]
variable = match_score: Number
variable = response_time: Duration
variable = success_rate: Percentage
variable = recent_matches: List[Match]
variable = cache_ttl: 24_hours
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    variable = all_donors: Array[Donor]
    variable = matching_results: List[Match]
    variable = compatibility_score: Number
    variable = distance_km: Number
    variable = confidence_level: Percentage
</agent>
```

---

### 8. function
**Purpose:** Custom logic and operations specific to agent

```
function = match_donors_with_requests()
function = calculate_compatibility_score()
function = filter_by_distance()
function = rank_matches()
function = send_notification()
function = store_match_record()
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    function = filter_verified_donors()
        REQUIREMENT: donor.verified == true
        REQUIREMENT: donor.age >= 18
        REQUIREMENT: donor.last_donation < 56_days
    
    function = calculate_score(donor, request)
        CONSIDER: blood_type_compatibility 40%
        CONSIDER: distance 30%
        CONSIDER: donor_rating 20%
        CONSIDER: availability 10%
        RETURN: score between 0-100
    
    function = rank_matches(scores)
        ORDER: by score descending
        LIMIT: top 5 matches
        RETURN: ranked list
</agent>
```

---

### 9. create
**Purpose:** What agent generates or creates

```
create = match_recommendations
create = classification_results
create = optimization_rankings
create = booking_confirmations
create = alert_notifications
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    create = match_results
        CONTAINS: request_id
        CONTAINS: donor_list
        CONTAINS: compatibility_scores
        CONTAINS: distance_km
        CONTAINS: timestamp
</agent>
```

---

### 10. build
**Purpose:** How agent composes or assembles components

```
build = assemble_notifications(donor_list)
build = compose_recommendation_response()
build = construct_match_package()
build = prepare_booking_summary()
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    build = assemble_notifications(matches)
        STEP-1: prepare_message_template()
        STEP-2: fill_with_donor_data()
        STEP-3: add_action_buttons()
        STEP-4: validate_message_format()
        RETURN: ready_to_send_notification
</agent>
```

---

### 11. process
**Purpose:** Reasoning and decision-making logic

```
process = WORKFLOW {
    STEP-1: observe_input()
    STEP-2: evaluate_conditions()
    STEP-3: apply_logic()
    STEP-4: determine_action()
}

process = DECISION {
    IF condition_A THEN action_A
    IF condition_B THEN action_B
    DEFAULT action_default
}
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    process = WORKFLOW {
        STEP-1: obtain_donor_list()
        STEP-2: obtain_request_list()
        STEP-3: filter_eligible_donors()
        STEP-4: calculate_compatibility_scores()
        STEP-5: rank_by_score()
        STEP-6: prepare_recommendations()
    }
    
    process = DECISION {
        IF matches_found > 0
            THEN prepare_top_5_matches()
        IF matches_found == 0
            THEN prepare_fallback_options()
        DEFAULT notify_insufficient_matches()
    }
</agent>
```

---

### 12. alter
**Purpose:** Transformations and modifications applied by agent

```
alter = normalize_data_format
alter = transform_values
alter = filter_by_criteria
alter = aggregate_results
alter = enrich_with_context
alter = anonymize_sensitive_fields
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    alter = normalize_location_to_coordinates()
    alter = filter_by_distance_radius(10_km)
    alter = enrich_donor_with_rating()
    alter = anonymize_phone_numbers()
</agent>
```

---

### 13. manage
**Purpose:** Resource allocation and agent lifecycle management

```
manage = max_concurrent_executions = 10
manage = timeout_duration = 5_minutes
manage = retry_policy = exponential_backoff
manage = memory_limit = 512_MB
manage = cpu_allocation = 2_cores
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    manage = max_concurrent_executions = 50
    manage = timeout_duration = 5_seconds
    manage = retry_policy = exponential_backoff(max_3_attempts)
    manage = memory_limit = 256_MB
</agent>
```

---

### 14. monitor
**Purpose:** Observability, metrics, and tracking

```
monitor = metric(total_operations)
monitor = metric(success_rate)
monitor = metric(response_time)
monitor = metric(error_count)
monitor = alert(threshold_exceeded)
monitor = log(all_decisions)
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    monitor = metric(total_matches_found)
    monitor = metric(success_rate_percentage)
    monitor = metric(response_time_ms)
    monitor = metric(false_match_rate)
    monitor = alert(response_time > 5_seconds)
    monitor = alert(false_match_rate > 1%)
    monitor = log(all_matching_decisions)
</agent>
```

---

### 15. execute
**Purpose:** Actions the agent takes (what it actually does)

```
execute = send_notification(donor_list)
execute = store_result(database)
execute = broadcast_update(websocket)
execute = trigger_next_agent(agentic_system)
execute = record_event(audit_log)
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    execute = send_notifications(to_matched_donors)
    execute = store_match_results(in_database)
    execute = broadcast_to_frontend(via_websocket)
    execute = trigger_booking_agent(with_selected_match)
    execute = record_match_event(in_audit_log)
</agent>
```

---

### 16. protect
**Purpose:** Security and access controls

```
protect = require_authentication()
protect = require_authorization(role)
protect = encrypt_sensitive_data(field)
protect = audit_all_actions()
protect = rate_limit(requests_per_minute)
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    protect = require_authentication()
    protect = require_authorization(service_account)
    protect = encrypt_sensitive_data(phone, email)
    protect = audit_all_actions()
    protect = rate_limit(1000_per_hour)
</agent>
```

---

### 17. maintain
**Purpose:** Memory, caching, and state management

```
maintain = cache(data_source, ttl)
maintain = memory(variable_name, duration)
maintain = persist(state_to_database)
maintain = clear_cache(on_condition)
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    maintain = cache(donor_list, 1_hour)
    maintain = cache(compatibility_rules, 24_hours)
    maintain = memory(recent_matches, last_100)
    maintain = persist(match_records_to_database)
    maintain = clear_cache(on_donor_status_change)
</agent>
```

---

### 18. collaborate
**Purpose:** Coordination with other agents

```
collaborate = receive_from(previous_agent)
collaborate = send_to(next_agent)
collaborate = wait_for(condition)
collaborate = resolve_conflict(by_strategy)
collaborate = share_memory(shared_variable)
```

**Example:**
```
<agent>
    agent_name = BookingAgent
    
    collaborate = receive_from(OptimizationAgent)
    collaborate = wait_for(user_confirmation)
    collaborate = resolve_conflict(by_priority_list)
    collaborate = share_memory(user_preferences)
    collaborate = send_to(NotificationAgent)
</agent>
```

---

### 19. rule
**Purpose:** Constraints and limits on agent behavior

```
rule = require(condition, error_message)
rule = constraint(name, validation_logic)
rule = limit(resource, max_value)
rule = forbid(dangerous_action)
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    rule = require(donor.verified == true)
    rule = require(donor.age >= 18)
    rule = require(donor.last_donation < 56_days)
    rule = constraint(compatibility_score, >= 0.95)
    rule = constraint(distance, <= 10_km)
    rule = limit(notifications_per_donor_per_day, 5)
    rule = limit(matches_per_request, 10)
    rule = forbid(contacting_unverified_donors)
</agent>
```

---

### 20. checkpoint
**Purpose:** Validation and verification points in agent execution

```
checkpoint = validate(condition, error_on_fail)
checkpoint = verify(data_integrity)
checkpoint = test(output_accuracy)
checkpoint = ensure(intent_alignment)
```

**Example:**
```
<agent>
    agent_name = DonorMatcher
    
    checkpoint = INTENT_ALIGNMENT
        VERIFY: output matches agent INTENT
        VERIFY: no hallucinated data
        VERIFY: accuracy >= 95%
    
    checkpoint = DATA_VALIDITY
        VERIFY: all donors verified
        VERIFY: eligible by age/donation_gap
        VERIFY: coordinates valid
    
    checkpoint = COMPATIBILITY_RULES
        VERIFY: blood type matches
        VERIFY: distance within range
        VERIFY: availability confirmed
    
    checkpoint = OUTPUT_FORMAT
        VERIFY: all required fields present
        VERIFY: no sensitive data exposed
        VERIFY: timestamp accurate
</agent>
```

---

## AGENTIC SYNTAX

### Complete Agentic Structure

```
<agentic>
    agentic_name = system_identifier
    
    TOKEN_LIMIT = maximum_total_tokens
    TOKEN_MIN = minimum_tokens_needed
    TOKEN_MAX = maximum_per_operation
    
    environment = deployment_environment
    
    agents = [agent_1, agent_2, agent_3]
    
    intent = collective_system_goal
    
    data = <data_sources_shared_by_agents>
    
    variable = shared_system_variables
    
    function = shared_system_functions
    
    scheduling = execution_scheduling_rules
    
    collaborate = coordination_strategy
    
    checkpoint = system_level_validation
    
    rule = global_constraints
    
    protect = system_level_security
    
    monitor = system_metrics_and_alerts
    
    maintain = system_state_management
    
</agentic>
```

### Minimal Agentic System

```
<agentic>
    agentic_name = SmartTravelPlanner
    
    agents = [intent_agent, search_agent, optimization_agent, booking_agent]
    
    intent = Coordinate agents to provide end-to-end travel booking
    
    collaborate = sequential
    
    checkpoint = all_checkpoints_pass_before_next_step
</agentic>
```

---

## AGENTIC KEYWORDS

### 1-3. TOKEN_LIMIT, TOKEN_MIN, TOKEN_MAX
**Purpose:** Total token budgets for entire agentic system

```
TOKEN_LIMIT = 100000       // Total for all agents
TOKEN_MIN = 20000          // Minimum needed for safe operation
TOKEN_MAX = 120000         // Hard limit
```

---

### 4. agentic_name
**Purpose:** System-level identifier

```
agentic_name = SmartTravelPlanner
agentic_name = BloodMatchingSystem
agentic_name = WeatherAlertSystem
```

---

### 5. environment
**Purpose:** Deployment context for entire system

```
environment = production
environment = staging
environment = development
```

---

### 6. agents
**Purpose:** List of agents in the system

```
agents = [intent_agent, search_agent, optimization_agent, booking_agent]
agents = [donor_matcher, urgency_prioritizer, notification_agent]
```

---

### 7. intent
**Purpose:** Collective purpose of agent system

```
intent = Coordinate travel booking across 4 agents
intent = Match blood donors with urgent requests efficiently
intent = Provide real-time weather monitoring with alerts
```

---

### 8. data
**Purpose:** Shared data sources accessible to all agents

```
<data>
    data_name = user_preferences
    data_name = shared_cache
    data_name = system_state
</data>
```

---

### 9. variable
**Purpose:** System-level shared variables

```
variable = shared_user_context
variable = system_state
variable = shared_cache
```

---

### 10. function
**Purpose:** Shared functions available to all agents

```
function = calculate_score()
function = validate_data()
function = log_event()
```

---

### 11. scheduling
**Purpose:** How agents execute and when

```
scheduling = sequential          // One after another
scheduling = parallel            // All simultaneously
scheduling = event_driven        // Based on events
scheduling = hierarchical        // Master-worker
```

**Example:**
```
<agentic>
    agentic_name = SmartTravelPlanner
    
    scheduling = sequential
        STEP-1: intent_agent
        STEP-2: search_agent (parallel: flights, hotels, activities)
        STEP-3: optimization_agent
        STEP-4: booking_agent
</agentic>
```

---

### 12. collaborate
**Purpose:** How agents coordinate and communicate

```
collaborate = sequential_handoff
    AGENT-1 -> AGENT-2 -> AGENT-3

collaborate = parallel_execution
    AGENT-1, AGENT-2, AGENT-3 (concurrent)

collaborate = event_driven
    EVENT triggers AGENT

collaborate = consensus_based
    AGENTS vote on decision

collaborate = shared_memory
    AGENTS access SHARED_STATE
```

---

### 13. checkpoint
**Purpose:** System-level validation points

```
checkpoint = SYSTEM_LEVEL
    AT_STEP: 1, 2, 3, 4
    VERIFY: intent_alignment
    VERIFY: data_consistency
    VERIFY: all_agents_successful

checkpoint = INTER_AGENT
    BETWEEN: agent_A and agent_B
    VERIFY: data_format
    VERIFY: required_fields
```

**Example:**
```
<agentic>
    agentic_name = SmartTravelPlanner
    
    checkpoint = AFTER_STEP_1
        VERIFY: user_preferences_complete
        VERIFY: all_required_fields_filled
    
    checkpoint = AFTER_STEP_2
        VERIFY: search_results_available
        VERIFY: all_three_searches_complete
    
    checkpoint = AFTER_STEP_3
        VERIFY: ranking_complete
        VERIFY: results_within_budget
    
    checkpoint = AFTER_STEP_4
        VERIFY: booking_confirmed
        VERIFY: confirmation_sent_to_user
</agentic>
```

---

### 14. rule
**Purpose:** Global constraints for all agents

```
rule = require(system_level_constraint)
rule = forbid(dangerous_system_action)
rule = all_agents_must(follow_policy)
```

---

### 15. protect
**Purpose:** System-level security

```
protect = require_authentication()
protect = encrypt_all_data()
protect = audit_all_operations()
```

---

### 16. monitor
**Purpose:** System-level metrics and alerts

```
monitor = metric(end_to_end_success_rate)
monitor = metric(total_system_latency)
monitor = alert(any_agent_fails)
monitor = log(all_agent_decisions)
```

---

### 17. maintain
**Purpose:** System-level state and memory

```
maintain = shared_cache
maintain = system_state_database
maintain = inter_agent_memory
```

---

## COMPLETE EXAMPLES

### Example 1: Blood Donation Matching System

```
<agentic>
    agentic_name = BloodMatchingSystem
    
    TOKEN_LIMIT = 150000
    TOKEN_MIN = 50000
    TOKEN_MAX = 180000
    
    environment = production
    
    agents = [donor_matcher, urgency_prioritizer, notification_agent]
    
    intent = Match blood donors with urgent requests efficiently and safely
    
    <data>
        data_name = donors
        data_name = requests
        data_name = shared_matches
    </data>
    
    variable = active_matches
    variable = system_state
    variable = shared_cache
    
    function = calculate_urgency_score()
    function = validate_match_integrity()
    function = send_notifications()
    
    scheduling = sequential
        STEP-1: urgency_prioritizer (prioritize requests)
        STEP-2: donor_matcher (find matching donors)
        STEP-3: notification_agent (notify selected donors)
    
    collaborate = sequential_handoff
        urgency_prioritizer -> donor_matcher -> notification_agent
        shared_memory: active_matches, system_state
    
    checkpoint = AFTER_URGENCY_PRIORITIZATION
        VERIFY: requests_ranked_correctly
        VERIFY: urgent_requests_first
    
    checkpoint = AFTER_MATCHING
        VERIFY: matches_meet_requirements
        VERIFY: accuracy_threshold_met
        VERIFY: no_hallucinated_donors
    
    checkpoint = AFTER_NOTIFICATION
        VERIFY: all_donors_contacted
        VERIFY: responses_recorded
    
    rule = require(system_level_intent_alignment)
    rule = forbid(contacting_unverified_donors)
    rule = all_agents_must(maintain_data_privacy)
    
    protect = require_authentication()
    protect = encrypt_sensitive_data(phone, email, health_info)
    protect = audit_all_matching_decisions()
    
    monitor = metric(successful_matches_count)
    monitor = metric(system_latency_seconds)
    monitor = metric(match_accuracy_percentage)
    monitor = alert(any_agent_fails)
    monitor = alert(accuracy_drops_below_95%)
    
    maintain = shared_cache(donor_list, 1_hour)
    maintain = persist_matches_to_database()
    
</agentic>
```

### Example 2: Smart Travel Planning System

```
<agentic>
    agentic_name = SmartTravelPlanner
    
    TOKEN_LIMIT = 200000
    TOKEN_MIN = 75000
    TOKEN_MAX = 250000
    
    environment = production
    
    agents = [intent_agent, search_agent, optimization_agent, booking_agent]
    
    intent = Provide end-to-end travel booking with personalization and optimization
    
    <data>
        data_name = user_preferences
        data_name = flight_results
        data_name = hotel_results
        data_name = activity_results
        data_name = optimized_plan
    </data>
    
    variable = user_context
    variable = search_results
    variable = optimized_selections
    
    function = score_compatibility()
    function = rank_by_preferences()
    function = validate_booking()
    
    scheduling = sequential
        STEP-1: intent_agent (gather preferences)
        STEP-2: search_agent (parallel: flights, hotels, activities)
        STEP-3: optimization_agent (rank by preferences)
        STEP-4: booking_agent (execute booking)
    
    collaborate = sequential_with_parallel_phase
        intent_agent -> [search_agent parallel] -> optimization_agent -> booking_agent
        SHARED_MEMORY: user_context, results, selections
    
    checkpoint = AFTER_INTENT_COLLECTION
        VERIFY: user_preferences_complete
        VERIFY: dates_valid_and_future
        VERIFY: budget_specified_and_valid
    
    checkpoint = AFTER_SEARCH
        VERIFY: flight_results_available
        VERIFY: hotel_results_available
        VERIFY: activity_results_available
        VERIFY: results_within_budget_range
    
    checkpoint = AFTER_OPTIMIZATION
        VERIFY: all_options_ranked
        VERIFY: total_cost_within_budget
        VERIFY: top_recommendations_diverse
    
    checkpoint = AFTER_BOOKING
        VERIFY: all_confirmations_received
        VERIFY: payment_processed
        VERIFY: confirmation_sent_to_user
    
    rule = require(budget_constraint_respected)
    rule = forbid(booking_expired_options)
    rule = all_agents_must(verify_data_integrity)
    
    protect = require_user_authentication()
    protect = encrypt_payment_information()
    protect = audit_all_bookings()
    
    monitor = metric(end_to_end_success_rate)
    monitor = metric(average_system_latency)
    monitor = metric(user_satisfaction_score)
    monitor = alert(booking_success_rate_below_95%)
    monitor = alert(system_latency_exceeds_5_minutes)
    
    maintain = cache(search_results, 5_minutes)
    maintain = persist_bookings_to_database()
    maintain = clean_expired_cache_entries()
    
</agentic>
```

---

## BEST PRACTICES

### 1. Clear Intent Declaration
```
✅ intent = Match donors with requests efficiently
❌ intent = do stuff
```

### 2. Explicit Variable Declaration
```
✅ variable = match_score: Number
❌ variable = data
```

### 3. Define Checkpoints at Every Step
```
✅ checkpoint = validate_all_required_fields()
❌ Assume data is valid
```

### 4. Govern with Rules
```
✅ rule = require(donor.verified == true)
✅ rule = forbid(unethical_action)
❌ Hope agent does right thing
```

### 5. Monitor Everything
```
✅ monitor = metric(success_rate)
✅ monitor = alert(threshold_exceeded)
❌ Silent execution
```

### 6. Protect Sensitive Operations
```
✅ protect = encrypt_sensitive_data()
✅ protect = audit_all_actions()
❌ Unprotected data access
```

---

## QUICK REFERENCE

### Agent Checklist

- [ ] TOKEN_LIMIT set (and TOKEN_MIN/TOKEN_MAX)
- [ ] agent_name assigned
- [ ] environment specified
- [ ] Data sources declared in <data>
- [ ] intent clearly stated
- [ ] variables declared
- [ ] custom functions defined
- [ ] process described (WORKFLOW and DECISION)
- [ ] create/build specified
- [ ] execute actions listed
- [ ] protect security controls set
- [ ] maintain memory/cache configured
- [ ] rule constraints defined
- [ ] checkpoint validations set
- [ ] monitor metrics configured
- [ ] collaborate with other agents defined

### Agentic Checklist

- [ ] agentic_name assigned
- [ ] TOKEN limits set
- [ ] agents list complete
- [ ] intent clearly stated
- [ ] shared data defined
- [ ] scheduling strategy chosen
- [ ] collaboration method defined
- [ ] system checkpoints set
- [ ] global rules defined
- [ ] system-level security configured
- [ ] system metrics monitoring setup
- [ ] state persistence configured


