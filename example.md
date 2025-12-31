IMPORTS {
    format.web
    format.mobile
    architecture.microservices
    development_plan.agile.kanban_model
    compliance.gdpr
    component.frontend
    component.backend
    component.api
    component.database
    component.messaging
}

CONFIG {
    token_limit = 100000
    tech_stack = react_js, typescript, fastapi, python, postgresql, redis
    target_environment = production
    performance_tier = enterprise
    security_level = strict
    testing_coverage = 95%
    max_latency_ms = 200
    max_users = 500000
    auto_scaling = enabled
    monitoring = prometheus, grafana, datadog
}

AGENT {
    
    agent Donor_Availability_Agent {
        environment = mobile_app, web_app
        data_source = database.donors, location_service
        
        decision {
            workflow {
                step_1: receive_location_update
                step_2: calculate_distance_to_requests
                step_3: fetch_nearby_blood_requests
                step_4: match_blood_type
                step_5: notify_donor_of_matches
                step_6: log_notification_event
            }
        }
        
        memory {
            short_term = 10000_notifications
            long_term = database.notification_history
        }
        
        skills = [
            fetch_location,
            calculate_distance,
            query_requests,
            match_blood_type,
            send_push_notification,
            log_event
        ]
        
        safety = [
            max_concurrent: 10000,
            timeout: 5s,
            rate_limit: 100000req/min
        ]
    }
    
    agent Request_Fulfillment_Agent {
        environment = hospital_system, emergency_services
        data_source = database.requests, database.donors, blood_bank
        
        decision {
            workflow {
                step_1: receive_blood_request
                step_2: classify_urgency {
                    CRITICAL: "immediate_alert_all_donors"
                    URGENT: "alert_nearby_donors"
                    NORMAL: "schedule_regular_request"
                }
                step_3: find_matching_donors
                step_4: coordinate_collection
                step_5: update_blood_bank_inventory
                step_6: send_fulfillment_confirmation
            }
        }
        
        memory {
            short_term = 50000_requests
            long_term = database.request_history
        }
        
        skills = [
            receive_request,
            classify_urgency,
            find_donors,
            coordinate_collection,
            update_inventory,
            send_confirmation
        ]
        
        safety = [
            max_concurrent: 5000,
            timeout: 30s,
            verification_required: true,
            data_privacy: gdpr_compliant
        ]
    }
}

DATA {
    
    data API_KEYS {
        type = secure_vault
        access = private
        encryption = aes256_kms
        keys = [
            twilio_key,
            firebase_key,
            stripe_key,
            mapbox_key,
            openai_key
        ]
    }
    
    data User_Database {
        type = postgresql
        location = prod-db.aws.com
        schema = {
            id: uuid,
            name: string,
            email: string,
            phone: string,
            blood_type: enum[O+, O-, A+, A-, B+, B-, AB+, AB-],
            location: coordinates,
            user_type: enum[donor, recipient, hospital, admin],
            verified: boolean,
            created_at: timestamp,
            last_donation: timestamp
        }
        access = authenticated
        encryption = tls_transit, aes256_rest
    }
    
    data Blood_Request_Database {
        type = postgresql
        location = prod-db.aws.com
        schema = {
            id: uuid,
            hospital_id: uuid,
            blood_type: string,
            quantity: integer,
            urgency: enum[critical, urgent, normal],
            location: coordinates,
            status: enum[open, in_progress, fulfilled, cancelled],
            created_at: timestamp,
            expires_at: timestamp
        }
        access = authenticated
        encryption = tls_transit, aes256_rest
    }
    
    data Donor_Location_Cache {
        type = redis
        location = cache.aws.com
        ttl = 60_seconds
        access = authenticated
        encryption = tls_transit
    }
}

PAGE Home {
    
    FRONTEND {
        layout = center
        components = [
            navbar_with_auth,
            hero_banner,
            quick_stats,
            cta_button_donate,
            recent_requests_feed,
            impact_metrics,
            footer
        ]
        animations = enabled
        responsive = mobile_first
        accessibility = wcag2.1_aa
        dark_mode = enabled
    }
    
    BACKEND {
        scale = 500000_users
        network = global
        performance = high_concurrency
        logic = feature_based_containers
        database = postgresql
        cache = redis
        message_queue = kafka
    }
    
    API {
        latency = <200ms
        speed = high
        robustness = strong
        seamless = true
        endpoints = [
            GET /api/requests/active,
            GET /api/donors/nearby,
            GET /api/stats/impact,
            POST /api/donations/create
        ]
    }
    
    INTENT {
        "Landing page for blood donation platform. Real-time display 
         of active blood requests, nearby donors, impact metrics, and 
         one-click donation signup. Designed for all ages and 
         technical backgrounds."
    }
    
    THEME {
        colors = red, white, gray
        style = modern, warm, accessible
        typography = clean_sans_serif
        spacing = generous
    }
    
    BUILD {
        framework = react_js
        state_management = redux
        styling = tailwind_css
        animations = framer_motion
        experience = seamless_all_ages
        testing = jest, react_testing_library
        performance_target = lighthouse_95
    }
}

PAGE DonorDashboard {
    
    FRONTEND {
        layout = sidebar_main
        components = [
            sidebar_navigation,
            header_with_notifications,
            donation_history_table,
            upcoming_drives_calendar,
            impact_stats,
            eligibility_checker,
            health_questionnaire
        ]
        animations = enabled
        responsive = adaptive
        dark_mode = enabled
    }
    
    BACKEND {
        scale = 100000_concurrent_users
        network = multi_region
        performance = ultra_fast
        logic = event_driven
        database = postgresql
        cache = redis_cluster
    }
    
    API {
        latency = <100ms
        speed = ultra_high
        robustness = critical
        seamless = true
        authentication = jwt
        rate_limiting = 50000_requests_per_min
    }
    
    INTENT {
        "Personal donor dashboard showing donation history, 
         upcoming drives, eligibility status, and impact metrics. 
         Mobile-optimized for quick access."
    }
    
    THEME {
        colors = blue, white, green_accent
        style = professional, data_focused
        typography = system_font_stack
        spacing = comfortable
    }
    
    BUILD {
        framework = react_js
        state_management = zustand
        styling = emotion
        charting = recharts
        experience = performance_critical
        testing = cypress
        performance_target = lighthouse_98
    }
}

PAGE HospitalRequestForm {
    
    FRONTEND {
        layout = center
        components = [
            form_header,
            blood_type_selector,
            quantity_input,
            urgency_selector,
            location_picker,
            doctor_verification,
            submit_button
        ]
        animations = enabled
        responsive = mobile_first
        accessibility = wcag2.1_aaa
    }
    
    BACKEND {
        scale = 50000_concurrent_requests
        network = multi_region
        performance = ultra_fast
        logic = event_driven
        database = postgresql
    }
    
    API {
        latency = <100ms
        speed = ultra_high
        robustness = critical
        seamless = true
        authentication = oauth2
        verification = doctor_credentials_required
    }
    
    INTENT {
        "Hospital blood request submission form with doctor verification,
         real-time availability lookup, and instant donor notifications."
    }
    
    THEME {
        colors = hospital_blue, white, urgent_red
        style = professional, clinical
        typography = readable_sans_serif
        spacing = clear_sections
    }
    
    BUILD {
        framework = react_js
        state_management = jotai
        styling = tailwind_css
        form_library = react_hook_form
        experience = zero_friction
        testing = vitest, react_testing_library
        performance_target = lighthouse_99
    }
}
