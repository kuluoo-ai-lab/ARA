# PAGE SYNTAX SPECIFICATION


## TABLE OF CONTENTS

1. [Overview](#overview)
2. [Core Definition](#core-definition)
3. [Structural Components](#structural-components)
4. [PAGE Declaration Syntax](#page-declaration-syntax)
5. [Detailed Specifications](#detailed-specifications)
6. [Data Binding](#data-binding)
7. [Examples](#examples)
8. [Error Handling](#error-handling)
9. [Best Practices](#best-practices)

---

## OVERVIEW

### What is a PAGE?

A **PAGE** is the primary compositional unit in the AI-native programming language. It represents a **self-contained, intent-driven execution environment** that unifies:

- **Presentation Logic** (Frontend UI)
- **Application Logic** (Backend Services)
- **Data Access** (Declared Sources)
- **Autonomous Intelligence** (Agents)
- **Governance & Safety** (Rules & Policies)

### PAGE Properties

| Property | Description |
|----------|-------------|
| **Scope** | All components within a PAGE are scoped to that PAGE |
| **Intent** | Single, immutable purpose declared at PAGE level |
| **Lifecycle** | Created on page load, destroyed on unload |
| **Composition** | PAGEs can contain other PAGEs |
| **Governance** | Rules, access controls, and compliance built-in |
| **Observable** | All operations are traceable and auditable |

### Why PAGE?

Traditional applications scatter logic across files:
```
❌ UI Code (React)
❌ Backend Code (Node.js)
❌ Data Models (MongoDB)
❌ Business Logic (Scattered)
❌ Agents (Async tasks)
❌ Security (Middleware)
```

PAGE unifies everything:
```
✅ PAGE declaration
   ├─ INTENT (purpose)
   ├─ <data> (sources)
   ├─ FRONT-END (UI)
   ├─ BACK-END (logic)
   ├─ <agent> (autonomy)
   ├─ RULE (constraints)
   ├─ PROTECT (security)
   ├─ MONITOR (observability)
   └─ MAINTAIN (state)
```

---

## CORE DEFINITION

### Basic PAGE Structure

```
DEFINITION page_name = [
    PAGE page_identifier {
        // PAGE content
    }
]
```

### Minimal PAGE Example

```
DEFINITION page_home = [
    PAGE home {
        INTENT {
            purpose: "Display home page to users"
        }
    }
]
```

### Complete PAGE Template

```
DEFINITION page_name = [
    PAGE page_identifier {
        
        // 1. DECLARE INTENT (MANI Keyword)
        INTENT { ... }
        
        // 2. DECLARE DATA SOURCES
        <data> { ... </data>
        
        // 3. DECLARE FRONTEND
        FRONT-END { ... }
        
        // 4. DECLARE BACKEND
        BACK-END { ... }
        
        // 5. DECLARE API
        API { ... }
        
        // 6. DECLARE AGENTS
        <agent> { ... </agent>
        
        // 7. DECLARE MULTI-AGENT COORDINATION
        <agentic> { ... </agentic>
        
        // 8. DECLARE RULES (MANI Keyword)
        RULE { ... }
        
        // 9. DECLARE PROTECTION (MANI Keyword)
        PROTECT { ... }
        
        // 10. DECLARE MONITORING (MANI Keyword)
        MONITOR { ... }
        
        // 11. DECLARE MAINTENANCE (MANI Keyword)
        MAINTAIN { ... }
        
        // 12. DECLARE MANAGEMENT (MANI Keyword)
        MANAGE { ... }
    }
]
```

---

## STRUCTURAL COMPONENTS

### 1. INTENT Block

**Purpose:** Declare the immutable purpose of the PAGE

**Syntax:**
```
INTENT {
    purpose: "String describing main goal"
    objective: "String describing desired outcome"
    boundary: "String describing limitations/constraints"
    [scope]: "String describing operational scope"
    [user_types]: [list of user types who use this PAGE]
    [success_criteria]: [list of success metrics]
}
```

**Properties:**
- **Immutable:** Cannot change during PAGE execution
- **Required:** Yes (every PAGE needs INTENT)
- **Validates:** All decisions verified against this

**Example:**
```
INTENT {
    purpose: "Provide weather information to users"
    objective: "Display accurate, real-time weather data"
    boundary: "Data must be from verified weather services"
    scope: "Global coverage, all regions"
    user_types: ["web_users", "mobile_users", "api_consumers"]
    success_criteria: [
        "Data accuracy > 95%",
        "Response time < 2 seconds",
        "Uptime > 99.9%"
    ]
}
```

---

### 2. <data> Element

**Purpose:** Declare all data sources accessible within the PAGE

**Syntax:**
```
<data>
    <data_identifier>
        source: [source_type]
        type: [data_type_specification]
        access: [access_control]
        cache: [cache_duration | "never"]
        scope: [page | global | session]
        encryption: [encryption_type]
        retention: [retention_period]
    </data_identifier>
    
    // Multiple data sources allowed
    <data_identifier_2>
        ...
    </data_identifier_2>
</data>
```

**Source Types:**
```
source: Database("connection_string")
source: API("endpoint_url")
source: Session()
source: Storage("location")
source: Stream("stream_identifier")
source: Cache("cache_key")
source: Environment("variable_name")
```

**Data Type Specifications:**
```
type: String
type: Number
type: Boolean
type: Object
type: Array[T]
type: Schema("schema_definition")
type: TimeSeries[field1, field2, ...]
type: Custom("custom_type_name")
```

**Access Control:**
```
access: public                           // No restrictions
access: private                          // Only PAGE itself
access: RULE(condition)                  // Custom rule
access: PROTECT(authentication_required) // Security gated
```

**Example:**
```
<data>
    <weather_data>
        source: API("https://api.weather.service/v1")
        type: TimeSeries[temperature, humidity, wind_speed]
        access: PROTECT(api_key_required)
        cache: 5_minutes
        scope: global
        encryption: "TLS_1.3"
        retention: "30_days"
    </weather_data>
    
    <user_preferences>
        source: Database("users_db")
        type: Object
        access: RULE(owner_id == user.id)
        cache: "never"
        scope: session
        encryption: "AES_256"
        retention: "90_days"
    </user_preferences>
    
    <location_data>
        source: Session()
        type: { lat: Number, lon: Number }
        access: private
        cache: 1_hour
        scope: session
        encryption: "none"
        retention: "session_only"
    </location_data>
</data>
```

---

### 3. FRONT-END Block

**Purpose:** Declare user-facing UI components and interactions

**Syntax:**
```
FRONT-END {
    layout: [layout_specification]
    theme: [theme_configuration]
    
    component ComponentName {
        data: bind(data_source)
        properties: { ... }
        events: { ... }
        styles: { ... }
    }
    
    // Multiple components allowed
    component ComponentName2 {
        ...
    }
}
```

**Layout Types:**
```
layout: responsive
layout: grid(columns, rows)
layout: flex(direction, justify, align)
layout: fixed(width, height)
layout: container(max_width)
```

**Component Declaration:**
```
component MetricsChart {
    data: bind(weather_data)
    type: LineChart
    properties: {
        x_axis: "time",
        y_axis: "temperature",
        title: "Temperature Trends",
        responsive: true
    }
    events: {
        on_hover: agent.show_details,
        on_click: agent.open_details_panel
    }
    styles: {
        color_scheme: "cool",
        height: "400px",
        margin: "16px"
    }
}
```

**Example:**
```
FRONT-END {
    layout: responsive
    theme: { primary_color: "#3498db", secondary_color: "#e74c3c" }
    
    component Header {
        data: bind(user_preferences)
        type: NavigationBar
        properties: {
            sticky: true,
            logo: "attached_logo.png",
            show_search: true
        }
        events: {
            on_search: agent.handle_search
        }
    }
    
    component MainContent {
        layout: grid(2, 1)
        
        component WeatherDisplay {
            data: bind(weather_data)
            type: Card
            properties: {
                show_details: true,
                units: "celsius"
            }
        }
        
        component LocationSelector {
            data: bind(location_data)
            type: MapComponent
            properties: {
                zoom: 10,
                interactive: true
            }
            events: {
                on_location_change: agent.update_weather
            }
        }
    }
    
    component Footer {
        type: StaticContent
        properties: {
            content: "© 2025 Weather App"
        }
    }
}
```

---

### 4. BACK-END Block

**Purpose:** Declare server-side logic, services, and computations

**Syntax:**
```
BACK-END {
    service ServiceName {
        endpoint: "/api/endpoint"
        method: [GET | POST | PUT | DELETE]
        authentication: [auth_type]
        compute: [logic_specification]
        response: [response_type]
        error_handling: { ... }
        cache: [cache_duration]
    }
    
    // Multiple services allowed
}
```

**Service Definition:**
```
service weather_service {
    endpoint: "/api/weather"
    method: GET
    authentication: "API_KEY"
    compute: {
        fetch_data_from_source()
        transform_to_schema()
        apply_filters()
        sort_by_date()
    }
    response: Object
    error_handling: {
        on_failure: return_cached_data()
    }
    cache: 5_minutes
}
```

**Example:**
```
BACK-END {
    service fetch_weather {
        endpoint: "/api/weather"
        method: GET
        authentication: "Bearer"
        compute: {
            // Receive location from frontend
            location = get_location_from_request()
            
            // Fetch from API
            raw_data = call_weather_api(location)
            
            // Transform
            formatted_data = transform(raw_data, schema)
            
            // Enrich with cache
            enriched = add_historical_data(formatted_data)
            
            // Return
            return enriched
        }
        response: Object
        error_handling: {
            on_api_failure: return_cached_data(),
            on_timeout: return_error_response(504)
        }
        cache: 5_minutes
    }
    
    service update_preferences {
        endpoint: "/api/preferences"
        method: POST
        authentication: "JWT"
        compute: {
            preferences = get_request_body()
            validate(preferences)
            store_in_database(preferences)
            return success_response()
        }
        response: Object
        error_handling: {
            on_validation_error: return_error_response(400)
        }
        cache: "never"
    }
    
    service search {
        endpoint: "/api/search"
        method: GET
        authentication: "API_KEY"
        compute: {
            query = get_query_parameter("q")
            results = search_database(query)
            return results
        }
        response: Array[Object]
        error_handling: {
            on_empty_results: return_empty_array()
        }
        cache: 10_minutes
    }
}
```

---

### 5. API Block

**Purpose:** Define external API integrations and contracts

**Syntax:**
```
API {
    integration IntegrationName {
        url: "endpoint_url"
        method: [GET | POST | PUT | DELETE]
        authentication: [auth_type]
        headers: { ... }
        request_schema: [schema]
        response_schema: [schema]
        retry_policy: { ... }
        timeout: [duration]
    }
}
```

**Example:**
```
API {
    integration weather_api {
        url: "https://api.weather.service/v1/current"
        method: GET
        authentication: "API_KEY"
        headers: {
            "Accept": "application/json",
            "User-Agent": "WeatherApp/1.0"
        }
        request_schema: {
            location: String,
            units: String
        }
        response_schema: {
            temperature: Number,
            humidity: Number,
            wind_speed: Number,
            condition: String
        }
        retry_policy: {
            max_retries: 3,
            backoff: "exponential",
            timeout: 5000
        }
        timeout: 5_seconds
    }
    
    integration geolocation_api {
        url: "https://api.geo.service/v1/reverse"
        method: GET
        authentication: "OAuth2"
        headers: {
            "Accept": "application/json"
        }
        request_schema: {
            latitude: Number,
            longitude: Number
        }
        response_schema: {
            address: String,
            city: String,
            country: String
        }
        timeout: 3_seconds
    }
}
```

---

## PAGE DECLARATION SYNTAX

### Complete Example: Blood Donation Platform

```
DEFINITION page_blood_donation_home = [
    PAGE home {
        
        // Import dependencies
        import: [
            "format.web",
            "architecture.modular",
            "compliance.international_standards"
        ]
        
        // Configure tech stack
        token_limit: 20000
        tech_stack: [
            "React",
            "HTML5",
            "CSS3",
            "MongoDB",
            "Express.js",
            "Node.js"
        ]
        
        // ════════════════════════════════════════
        // 1. DECLARE INTENT
        // ════════════════════════════════════════
        INTENT {
            purpose: "Connect blood donors with organizations needing blood"
            objective: "Facilitate life-saving blood donations"
            boundary: "All data must comply with medical privacy regulations"
            scope: "Global coverage with local compliance"
            user_types: ["donors", "blood_organizations", "administrators"]
            success_criteria: [
                "Matching accuracy > 95%",
                "Response time < 2 seconds",
                "Data security compliance 100%"
            ]
        }
        
        // ════════════════════════════════════════
        // 2. DECLARE DATA SOURCES
        // ════════════════════════════════════════
        <data>
            <donors>
                source: Database("mongodb://donors_db")
                type: Object
                access: PROTECT(authenticated_user)
                cache: 1_hour
                scope: global
                encryption: "AES_256"
                retention: "permanent"
            </donors>
            
            <blood_organizations>
                source: Database("mongodb://orgs_db")
                type: Object
                access: public
                cache: 24_hours
                scope: global
                encryption: "AES_256"
                retention: "permanent"
            </blood_organizations>
            
            <blood_requests>
                source: Database("mongodb://requests_db")
                type: Array[Object]
                access: PROTECT(public_with_privacy_filter)
                cache: 5_minutes
                scope: global
                encryption: "AES_256"
                retention: "90_days"
            </blood_requests>
            
            <user_location>
                source: Session()
                type: { latitude: Number, longitude: Number }
                access: private
                cache: "never"
                scope: session
                encryption: "TLS_1.3"
                retention: "session_only"
            </user_location>
        </data>
        
        // ════════════════════════════════════════
        // 3. DECLARE FRONTEND
        // ════════════════════════════════════════
        FRONT-END {
            layout: responsive
            theme: {
                primary_color: "#FF0000",
                secondary_color: "#FFFFFF",
                accent_color: "#DC143C"
            }
            
            component NavigationBar {
                type: Header
                data: bind(user_location)
                properties: {
                    sticky: true,
                    logo: "blood_donation_logo.png",
                    show_notifications: true
                }
                events: {
                    on_menu_click: agent.navigate_page
                }
            }
            
            component HeroSection {
                type: Hero
                properties: {
                    title: "Save Lives Through Blood Donation",
                    subtitle: "Find donors or blood organizations near you",
                    call_to_action: "Get Started",
                    background_image: "hero_blood_donation.jpg"
                }
                events: {
                    on_cta_click: agent.open_signup_modal
                }
            }
            
            component DonorFinder {
                type: SearchPanel
                data: bind(blood_organizations, user_location)
                properties: {
                    show_distance: true,
                    show_urgency: true,
                    allow_filters: true
                }
                events: {
                    on_search: agent.find_nearby_organizations,
                    on_select: agent.show_organization_details
                }
            }
            
            component RequestsList {
                type: CardList
                data: bind(blood_requests)
                properties: {
                    limit: 10,
                    show_urgency_badge: true,
                    sortable: true
                }
                events: {
                    on_card_click: agent.show_request_details,
                    on_donate_click: agent.open_donation_form
                }
            }
            
            component Footer {
                type: Footer
                properties: {
                    content: "© 2025 Blood Donation Network",
                    show_links: true,
                    show_social: true
                }
            }
        }
        
        // ════════════════════════════════════════
        // 4. DECLARE BACKEND
        // ════════════════════════════════════════
        BACK-END {
            service find_organizations {
                endpoint: "/api/organizations/nearby"
                method: GET
                authentication: "Optional"
                compute: {
                    location = get_location_from_request()
                    distance = get_distance_parameter(10)  // km
                    organizations = query_database(location, distance)
                    enrich_with_stats(organizations)
                    return organizations
                }
                response: Array[Object]
                error_handling: {
                    on_location_error: return_all_organizations(),
                    on_database_error: return_cached_data()
                }
                cache: 5_minutes
            }
            
            service get_blood_requests {
                endpoint: "/api/requests"
                method: GET
                authentication: "Optional"
                compute: {
                    filter = get_filters_from_request()
                    requests = query_database(filter)
                    sort_by_urgency(requests)
                    return requests
                }
                response: Array[Object]
                error_handling: {
                    on_empty: return_empty_array()
                }
                cache: 5_minutes
            }
            
            service create_donation_record {
                endpoint: "/api/donations"
                method: POST
                authentication: "JWT"
                compute: {
                    donation_data = get_request_body()
                    validate_donor(donation_data.donor_id)
                    validate_organization(donation_data.org_id)
                    save_to_database(donation_data)
                    trigger_notification(donation_data)
                    return success_response()
                }
                response: Object
                error_handling: {
                    on_validation_error: return_error_response(400),
                    on_database_error: return_error_response(500)
                }
                cache: "never"
            }
        }
        
        // ════════════════════════════════════════
        // 5. DECLARE API INTEGRATIONS
        // ════════════════════════════════════════
        API {
            integration geolocation_service {
                url: "https://api.maps.service/reverse-geocode"
                method: GET
                authentication: "API_KEY"
                request_schema: {
                    latitude: Number,
                    longitude: Number
                }
                response_schema: {
                    address: String,
                    city: String,
                    country: String
                }
                timeout: 3_seconds
            }
            
            integration notification_service {
                url: "https://api.notifications.service/send"
                method: POST
                authentication: "Bearer"
                request_schema: {
                    recipient_id: String,
                    message: String,
                    type: String
                }
                response_schema: {
                    status: String,
                    timestamp: String
                }
                timeout: 2_seconds
            }
        }
        
        // ════════════════════════════════════════
        // 6. DECLARE RULES (CONSTRAINTS)
        // ════════════════════════════════════════
        RULE {
            require(user.age >= 18, "Must be 18+ to donate blood")
            require(user.location_shared, "Must share location to find organizations")
            require(response_time < 2_seconds, "All responses must be < 2 seconds")
            require(data_accuracy > 0.95, "Blood type data must be 95%+ accurate")
            constraint("Blood type matching", blood_type_compatibility_check)
            constraint("Donor availability", donor_not_recently_donated)
        }
        
        // ════════════════════════════════════════
        // 7. DECLARE PROTECTION (SECURITY)
        // ════════════════════════════════════════
        PROTECT {
            authentication: "JWT + OAuth2"
            authorization: "Role-Based Access Control (RBAC)"
            encryption_in_transit: "TLS 1.3"
            encryption_at_rest: "AES-256-GCM"
            audit_log: "All access logged to immutable store"
            data_retention: "Personal data: 7 years, Medical data: 10 years"
            compliance_standards: [
                "HIPAA (Healthcare)",
                "GDPR (EU)",
                "PIPEDA (Canada)"
            ]
            pii_masking: true
            rate_limiting: "100 requests per minute per user"
        }
        
        // ════════════════════════════════════════
        // 8. DECLARE MONITORING
        // ════════════════════════════════════════
        MONITOR {
            metrics: [
                "response_time_p95",
                "error_rate",
                "cache_hit_ratio",
                "user_count_active",
                "donation_success_rate"
            ]
            
            checkpoints: [
                {
                    name: "Authentication",
                    condition: "user.authenticated == true",
                    severity: "critical"
                },
                {
                    name: "Data Validity",
                    condition: "blood_type in valid_blood_types",
                    severity: "critical"
                },
                {
                    name: "Privacy Compliance",
                    condition: "pii_not_leaked",
                    severity: "critical"
                }
            ]
            
            alerts: [
                {
                    condition: "response_time_p95 > 2_seconds",
                    severity: "warning",
                    action: "notify_devops"
                },
                {
                    condition: "error_rate > 1%",
                    severity: "critical",
                    action: "page_oncall"
                }
            ]
            
            dashboard: "built_in"
            data_export: "CSV, JSON"
        }
        
        // ════════════════════════════════════════
        // 9. DECLARE MAINTENANCE
        // ════════════════════════════════════════
        MAINTAIN {
            cache: {
                organizations: 24_hours,
                blood_requests: 5_minutes,
                user_preferences: 1_hour
            }
            
            session: {
                ttl: 24_hours,
                refresh_interval: 12_hours
            }
            
            database: {
                backup: "daily",
                backup_retention: "30_days",
                replication: "enabled"
            }
            
            consistency_model: "strong"
            
            data_cleanup: {
                expired_sessions: "hourly",
                old_logs: "monthly",
                inactive_users: "yearly"
            }
        }
        
        // ════════════════════════════════════════
        // 10. DECLARE MANAGEMENT
        // ════════════════════════════════════════
        MANAGE {
            lifecycle: {
                create: "on_page_load",
                operate: "while_user_active",
                destroy: "on_page_unload",
                cleanup: "automatic"
            }
            
            resource_limits: {
                memory: 512_MB,
                cpu: 2_cores,
                bandwidth: 100_MB_per_hour,
                database_connections: 10
            }
            
            scaling: {
                auto_scale: true,
                min_instances: 1,
                max_instances: 10,
                threshold: 80_percent_utilization
            }
        }
    }
]
```

---

## DATA BINDING

### Binding Data to Components

```
// Bind single data source
data: bind(donors)

// Bind multiple sources
data: bind(donors, blood_organizations)

// Bind with filters
data: bind(blood_requests, filter={urgent: true})

// Bind with transformation
data: bind(donors, transform=enrich_with_location)
```

### Dynamic Data Updates

```
component DonorList {
    data: bind(donors)
    
    // Update on data source change
    on_data_change: agent.refresh_list
    
    // Real-time updates
    real_time: true
    
    // Polling interval
    poll_interval: 30_seconds
}
```

---

## EXAMPLES

### Example 1: Simple Marketing Page

```
DEFINITION page_marketing = [
    PAGE marketing {
        INTENT {
            purpose: "Promote blood donation program"
            objective: "Increase donor awareness"
        }
        
        FRONT-END {
            layout: responsive
            
            component HeroSection {
                type: Hero
                properties: {
                    title: "Save Lives",
                    call_to_action: "Learn More"
                }
            }
            
            component InfoCards {
                type: CardGrid
                properties: {
                    cards: [
                        { title: "Quick", description: "Takes 15 minutes" },
                        { title: "Safe", description: "Fully screened" },
                        { title: "Important", description: "Saves 3 lives" }
                    ]
                }
            }
        }
        
        PROTECT {
            authentication: "none",
            encryption_in_transit: "TLS 1.3"
        }
    }
]
```

### Example 2: User Dashboard

```
DEFINITION page_donor_dashboard = [
    PAGE donor_dashboard {
        INTENT {
            purpose: "Show donor's donation history and impact"
            objective: "Encourage continued donations"
        }
        
        <data>
            <donation_history>
                source: Database("donations_db")
                type: Array[Object]
                access: PROTECT(owner_only)
                cache: 1_hour
            </donation_history>
            
            <impact_stats>
                source: Database("stats_db")
                type: Object
                access: PROTECT(owner_only)
                cache: 24_hours
            </impact_stats>
        </data>
        
        FRONT-END {
            component DonationHistory {
                data: bind(donation_history)
                type: Timeline
                properties: {
                    show_details: true
                }
            }
            
            component ImpactWidget {
                data: bind(impact_stats)
                type: StatCard
                properties: {
                    stats: ["lives_saved", "total_donations", "blood_type"]
                }
            }
        }
        
        PROTECT {
            authentication: "JWT",
            authorization: "owner_only"
        }
        
        MAINTAIN {
            cache: { donation_history: 1_hour }
        }
    }
]
```

---

## ERROR HANDLING

### Error Response Format

```
{
    "status": "error",
    "code": "ERROR_CODE",
    "message": "Human-readable error message",
    "details": { /* additional context */ },
    "timestamp": "ISO_8601_timestamp"
}
```

### Common Error Codes

```
INTENT_MISMATCH          → Output doesn't match declared intent
DATA_VALIDATION_ERROR    → Data doesn't match expected schema
AUTHENTICATION_FAILED    → User not authenticated
AUTHORIZATION_FAILED     → User lacks required permissions
DATA_NOT_FOUND          → Requested data doesn't exist
EXTERNAL_SERVICE_ERROR  → Third-party API failed
RATE_LIMIT_EXCEEDED     → Too many requests
INTERNAL_SERVER_ERROR   → Unrecoverable error
```

### Error Handling in Services

```
BACK-END {
    service fetch_data {
        endpoint: "/api/data"
        method: GET
        
        error_handling: {
            on_not_found: {
                status: 404,
                message: "Data not found",
                action: "return_error_response"
            },
            on_database_error: {
                status: 500,
                message: "Database error",
                action: "log_and_alert",
                fallback: "return_cached_data"
            },
            on_timeout: {
                status: 504,
                message: "Request timeout",
                action: "retry_with_backoff"
            }
        }
    }
}
```

---

## BEST PRACTICES

### 1. Always Declare Intent

```
✅ INTENT with clear purpose, objective, boundary
❌ Missing INTENT block
```

### 2. Declare Data Before Use

```
✅ <data> block declares all sources
   Then FRONT-END/BACK-END reference them
❌ Using data without declaring in <data>
```

### 3. Scope is Everything

```
✅ Explicit scope: scope: page | global | session
❌ Ambiguous scope
```

### 4. Protection First

```
✅ PROTECT block defined before using sensitive data
❌ Accessing sensitive data without PROTECT
```

### 5. Monitoring Checkpoints

```
✅ MONITOR with checkpoints for critical operations
❌ Silent failures without monitoring
```

### 6. Cache Strategically

```
✅ Cache rarely-changing data (24h), frequently-changing (5m), sensitive (never)
❌ Over-caching or under-caching
```

### 7. Error Handling

```
✅ Explicit error_handling in each service
❌ Missing error cases
```

### 8. Validation

```
✅ Validate at service boundary (BACK-END)
❌ Assuming data is valid
```

---

## COMPILATION NOTES

When compiled, a PAGE becomes:

1. **Frontend Code** (React components)
2. **Backend Code** (Express/Node services)
3. **Database Schema** (MongoDB collections)
4. **API Documentation** (OpenAPI spec)
5. **Deployment Config** (Docker, K8s manifests)
6. **Test Stubs** (Jest tests)
7. **Audit Trail** (Documentation of generation)

---

## REFERENCE

### Quick Syntax Cheat Sheet

```
PAGE name { }                          // Define page
INTENT { purpose, objective }          // Declare purpose
<data> ... </data>                     // Declare sources
FRONT-END { }                          // UI definition
BACK-END { }                           // Services definition
API { }                                // External APIs
RULE { require() }                     // Constraints
PROTECT { authentication, encryption } // Security
MONITOR { metrics, checkpoints }       // Observability
MAINTAIN { cache, session }            // State management
MANAGE { lifecycle, scaling }          // Resource control
<agent> ... </agent>                   // Autonomous agents
<agentic> ... </agentic>               // Multi-agent coordination
```
