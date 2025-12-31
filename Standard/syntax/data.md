# DATA SYNTAX SPECIFICATION 

---

## OVERVIEW

This DATA syntax uses **prompting-based declarations** (not code) where developers declare data requirements in structured, human-readable format.

### Core Principle
**"Declare WHAT data you need, WHERE it comes from, WHO can access it, and HOW to manage it"**

---

## DATA DECLARATION SYNTAX

### Complete Data Structure

```
<data>
    data_name = identifier
    
    connect = connection_type
    
    source = location_path
    
    environment = deployment_environment
    
    public/private = access_level
    
    create = schema_definition
    
    declare = variable_definitions
    
    use = usage_context
    
    alter = transformation_rules
    
    internal/external = data_location_type
    
    store = storage_specification
    
    checkpoint = validation_rules
    
    signal = event_triggers
    
    SEARCH = query_capabilities
    
</data>
```

### Minimal Data Declaration

```
<data>
    data_name = users
    connect = database
    source = mongodb://localhost:27017
    public/private = private
    create = User { id, name, email, phone }
    store = persistent
</data>
```

---

## KEYWORD DEFINITIONS & USAGE

### 1. data_name
**Purpose:** Unique identifier for the data source

```
data_name = donors
data_name = user_sessions
data_name = real_time_weather
data_name = search_results
```

**Rules:**
- Must be unique within PAGE
- Use snake_case naming
- Should be descriptive

---

### 2. connect
**Purpose:** Specify connection type/protocol

```
connect = database          // SQL/NoSQL database connection
connect = api              // REST/GraphQL API endpoint
connect = session          // User session storage
connect = cache            // In-memory or Redis cache
connect = storage          // Cloud storage (S3, GCS)
connect = stream           // Message queue (Kafka, RabbitMQ)
connect = environment      // Config/environment variables
connect = computed         // Derived/calculated data
```

**Examples:**
```
<data>
    data_name = donors
    connect = database
</data>

<data>
    data_name = flight_prices
    connect = api
</data>

<data>
    data_name = user_preferences
    connect = session
</data>
```

---

### 3. source
**Purpose:** Specify where data comes from (connection string/endpoint)

```
source = mongodb://user:pass@host:27017/database
source = postgresql://localhost:5432/myapp
source = https://api.service.com/v1/data
source = https://flights.api/search
source = redis://localhost:6379
source = s3://bucket-name/path
source = kafka://broker:9092/topic
source = SESSION()
source = ENVIRONMENT(VARIABLE_NAME)
source = COMPUTE(function_name)
```

**Examples:**
```
<data>
    data_name = donors
    connect = database
    source = mongodb://donors_db
</data>

<data>
    data_name = blood_requests
    connect = api
    source = https://hospital.api/blood-requests
</data>

<data>
    data_name = user_location
    connect = session
    source = SESSION()
</data>
```

---

### 4. environment
**Purpose:** Specify deployment context (where this data operates)

```
environment = production
environment = staging
environment = development
environment = testing
environment = local
environment = cloud
environment = hybrid
```

**Examples:**
```
<data>
    data_name = donation_records
    environment = production
    connect = database
</data>

<data>
    data_name = test_data
    environment = development
    connect = database
</data>
```

---

### 5. public/private
**Purpose:** Access control and data visibility

```
public/private = public              // Anyone can access
public/private = private             // Only declaring PAGE
public/private = protected           // Authenticated users
public/private = authenticated       // Logged-in users
public/private = authorized          // Specific roles
public/private = restricted          // Limited access
```

**Examples:**
```
<data>
    data_name = blood_availability
    public/private = public
</data>

<data>
    data_name = donor_health_records
    public/private = private
</data>

<data>
    data_name = user_preferences
    public/private = authenticated
</data>
```

---

### 6. create
**Purpose:** Define schema and structure of data

```
create = schema_name { field1, field2, field3 }
create = custom_structure_definition
create = inherited_from(existing_schema)
```

**Examples:**
```
<data>
    data_name = donors
    create = Donor {
        id,
        name,
        email,
        phone,
        blood_type,
        verified,
        last_donation,
        location
    }
</data>

<data>
    data_name = blood_requests
    create = BloodRequest {
        id,
        organization_id,
        blood_type,
        units_needed,
        urgency_level,
        deadline
    }
</data>

<data>
    data_name = matching_results
    create = MatchResult {
        request_id,
        donor_id,
        compatibility_score,
        distance_km,
        timestamp
    }
</data>
```

---

### 7. declare
**Purpose:** Define variables and their types used in data operations

```
declare = variable_name: type
declare = max_records: number
declare = timeout: duration
declare = retry_count: integer
```

**Examples:**
```
<data>
    data_name = donations
    declare = total_donations: number
    declare = success_rate: percentage
    declare = last_updated: timestamp
    declare = cache_ttl: 24_hours
</data>
```

---

### 8. use
**Purpose:** Specify where/how this data will be used

```
use = display_in_ui
use = send_notification
use = calculate_metrics
use = train_algorithm
use = filter_results
use = sort_results
use = aggregate_statistics
use = real_time_monitoring
```

**Examples:**
```
<data>
    data_name = donor_list
    use = display_in_ui
    use = filter_results
</data>

<data>
    data_name = matching_scores
    use = sort_results
    use = train_algorithm
</data>
```

---

### 9. alter
**Purpose:** Define transformations and modifications to data

```
alter = transform_values
alter = normalize_format
alter = aggregate_function
alter = filter_condition
alter = map_structure
alter = enrich_with_context
alter = anonymize_fields
```

**Examples:**
```
<data>
    data_name = raw_weather
    alter = normalize_temperature_to_celsius
    alter = enrich_with_location_name
    alter = filter_invalid_readings
</data>

<data>
    data_name = search_results
    alter = filter_by_budget_range
    alter = sort_by_price
    alter = enrich_with_ratings
</data>
```

---

### 10. internal/external
**Purpose:** Specify whether data is internal to system or comes from external sources

```
internal/external = internal       // Generated within system
internal/external = external       // From outside source
internal/external = hybrid         // Both internal and external
```

**Examples:**
```
<data>
    data_name = user_profiles
    internal/external = internal
</data>

<data>
    data_name = flight_options
    internal/external = external
</data>

<data>
    data_name = enriched_user_data
    internal/external = hybrid
</data>
```

---

### 11. store
**Purpose:** Where and how to persist data

```
store = persistent              // Save permanently
store = temporary               // Cache temporarily
store = session_only            // Only for session
store = request_only            // Only for request
store = memory                  // In-memory cache
store = database                // Database storage
store = distributed_cache       // Distributed cache
```

**Examples:**
```
<data>
    data_name = donation_history
    store = persistent
</data>

<data>
    data_name = recent_searches
    store = temporary
</data>

<data>
    data_name = shopping_cart
    store = session_only
</data>
```

---

### 12. checkpoint
**Purpose:** Validation and verification rules for data

```
checkpoint = validate_required_fields
checkpoint = check_data_types
checkpoint = verify_constraints
checkpoint = test_accuracy
checkpoint = ensure_consistency
checkpoint = authenticate_source
```

**Examples:**
```
<data>
    data_name = donors
    checkpoint = validate_required_fields(id, name, email)
    checkpoint = check_data_types(blood_type IN [A, B, AB, O])
    checkpoint = verify_age_constraints(age >= 18)
    checkpoint = ensure_unique(email)
</data>

<data>
    data_name = blood_requests
    checkpoint = validate_required_fields(blood_type, units)
    checkpoint = verify_deadline_future()
    checkpoint = check_urgency_valid()
</data>
```

---

### 13. signal
**Purpose:** Events and triggers related to data

```
signal = on_data_change
signal = on_threshold_exceeded
signal = on_error
signal = on_data_arrival
signal = on_cache_expire
signal = on_validation_fail
```

**Examples:**
```
<data>
    data_name = blood_inventory
    signal = on_threshold_exceeded TRIGGER alert_low_stock
    signal = on_data_change BROADCAST to_all_users
</data>

<data>
    data_name = urgent_requests
    signal = on_data_arrival NOTIFY matching_agent
</data>
```

---

### 14. SEARCH
**Purpose:** Query capabilities and search functionality

```
SEARCH = enable_full_text_search
SEARCH = enable_filtering
SEARCH = enable_sorting
SEARCH = enable_pagination
SEARCH = enable_aggregation
```

**Examples:**
```
<data>
    data_name = donor_directory
    SEARCH = enable_full_text_search(name, email)
    SEARCH = enable_filtering(blood_type, location, availability)
    SEARCH = enable_sorting(distance, rating, availability)
    SEARCH = enable_pagination(limit=50)
</data>

<data>
    data_name = blood_requests
    SEARCH = enable_filtering(urgency, blood_type, organization)
    SEARCH = enable_sorting(time_created, urgency_level)
</data>
```

---

## COMPLETE EXAMPLES

### Example 1: Blood Donation App Data

```
<data>
    data_name = donors
    connect = database
    source = mongodb://donors_db
    environment = production
    public/private = private
    create = Donor {
        id,
        name,
        email,
        phone,
        blood_type,
        verified,
        last_donation,
        health_status,
        location
    }
    declare = total_donors: number
    declare = active_donors: count
    use = display_in_ui
    use = filter_results
    alter = filter_verified_only
    alter = enrich_with_distance
    internal/external = internal
    store = persistent
    checkpoint = validate_required_fields(id, blood_type, email)
    checkpoint = verify_age(>= 18)
    checkpoint = check_last_donation(< 56 days)
    signal = on_data_change BROADCAST donor_list_updated
    SEARCH = enable_filtering(blood_type, location, availability)
    SEARCH = enable_sorting(distance, rating)
</data>

<data>
    data_name = blood_requests
    connect = api
    source = https://hospital.api/requests
    environment = production
    public/private = public
    create = BloodRequest {
        id,
        organization_id,
        blood_type,
        units_needed,
        urgency_level,
        deadline,
        location
    }
    declare = urgent_count: number
    declare = matching_success: percentage
    use = display_in_ui
    use = send_notification
    alter = prioritize_by_urgency
    alter = calculate_time_remaining
    internal/external = external
    store = temporary
    checkpoint = validate_blood_type()
    checkpoint = verify_deadline_future()
    checkpoint = check_units_positive()
    signal = on_data_arrival NOTIFY matching_agent
    SEARCH = enable_filtering(urgency, blood_type)
    SEARCH = enable_sorting(time_created)
</data>

<data>
    data_name = user_location
    connect = session
    source = SESSION()
    environment = production
    public/private = private
    create = Location {
        latitude,
        longitude,
        timestamp
    }
    declare = location_accuracy: meters
    declare = update_frequency: seconds
    use = filter_results
    use = calculate_metrics
    alter = anonymize_to_km_radius
    internal/external = internal
    store = session_only
    checkpoint = validate_coordinates()
    checkpoint = verify_recent_update()
    signal = on_data_change TRIGGER distance_calculation
    SEARCH = enable_sorting(distance)
</data>

<data>
    data_name = matching_results
    connect = computed
    source = COMPUTE(match_algorithm)
    environment = production
    public/private = authenticated
    create = MatchResult {
        request_id,
        donor_list,
        compatibility_score,
        distance_km,
        rank,
        confidence
    }
    declare = results_count: number
    declare = match_accuracy: percentage
    use = display_in_ui
    use = train_algorithm
    alter = rank_by_score
    alter = filter_by_threshold
    internal/external = internal
    store = temporary
    checkpoint = validate_match_accuracy()
    checkpoint = ensure_all_verified()
    signal = on_threshold_exceeded TRIGGER alert_low_matches
    SEARCH = enable_sorting(score, distance)
    SEARCH = enable_filtering(blood_type, distance)
</data>
```

### Example 2: Travel Booking Data

```
<data>
    data_name = user_preferences
    connect = session
    source = SESSION()
    environment = production
    public/private = private
    create = UserPreferences {
        source_location,
        destination,
        start_date,
        end_date,
        budget_min,
        budget_max,
        priority_factors,
        comfort_level
    }
    declare = trip_duration: days
    declare = daily_budget: currency
    use = filter_results
    use = calculate_metrics
    alter = normalize_dates
    alter = parse_locations
    internal/external = internal
    store = session_only
    checkpoint = validate_required_fields(source, destination, dates)
    checkpoint = verify_source_not_equal_destination()
    checkpoint = validate_budget_range()
    signal = on_data_change TRIGGER search_update
    SEARCH = enable_filtering()
</data>

<data>
    data_name = flight_options
    connect = api
    source = https://flights.api/search
    environment = production
    public/private = public
    create = Flight {
        airline,
        departure_time,
        arrival_time,
        price,
        duration,
        rating,
        seats_available
    }
    declare = results_count: number
    declare = price_range: currency
    use = display_in_ui
    use = sort_results
    alter = normalize_prices
    alter = calculate_duration
    internal/external = external
    store = temporary
    checkpoint = validate_times()
    checkpoint = verify_availability()
    signal = on_data_arrival BROADCAST search_complete
    SEARCH = enable_sorting(price, duration, rating)
    SEARCH = enable_filtering(airline, time)
</data>

<data>
    data_name = optimized_travel_plan
    connect = computed
    source = COMPUTE(optimization_algorithm)
    environment = production
    public/private = authenticated
    create = OptimizedPlan {
        rank,
        flight_option,
        hotel_option,
        activities,
        total_cost,
        score,
        confidence
    }
    declare = top_recommendations: count
    declare = match_score: percentage
    use = display_in_ui
    use = train_algorithm
    alter = rank_by_score
    alter = filter_within_budget
    internal/external = internal
    store = temporary
    checkpoint = verify_total_within_budget()
    checkpoint = ensure_options_available()
    signal = on_data_change TRIGGER ui_update
    SEARCH = enable_sorting(score, price)
</data>
```

---

## BEST PRACTICES

### 1. Declare Data First
```
✅ Declare all data in <data> block before using
❌ Assume data exists without declaration
```

### 2. Be Specific with Types
```
✅ create = User { id: UUID, name: String, email: Email }
❌ create = User { data }
```

### 3. Set Appropriate Storage
```
✅ Temporary data: store = temporary
✅ Persistent data: store = persistent
❌ Everything in session
```

### 4. Validate at Checkpoints
```
✅ checkpoint = validate_required_fields()
✅ checkpoint = verify_constraints()
❌ Silent failures
```

### 5. Signal Important Events
```
✅ signal = on_data_change BROADCAST updates
✅ signal = on_threshold_exceeded TRIGGER alert
❌ No notification of data changes
```

### 6. Enable Search When Needed
```
✅ SEARCH = enable_filtering(relevant_fields)
✅ SEARCH = enable_sorting(key_fields)
❌ No search capability
```

---

## QUICK REFERENCE

### Data Declaration Checklist

- [ ] data_name assigned (unique identifier)
- [ ] connect specified (database, api, session, etc.)
- [ ] source defined (connection string or endpoint)
- [ ] environment set (production, development, etc.)
- [ ] public/private configured (access control)
- [ ] create schema defined (structure and fields)
- [ ] declare variables if needed
- [ ] use context specified (how data is used)
- [ ] alter transformations defined
- [ ] internal/external marked
- [ ] store location specified
- [ ] checkpoint validations set
- [ ] signal events configured
- [ ] SEARCH capabilities enabled

---
