# DATA CODE GENERATION STANDARD
## AI-Native Programming Language - Data Implementation Guide


---

## OVERVIEW

This standard defines how to generate implementation code for DATA declarations in the AI-Native Language across multiple technology stacks and programming languages.

---

## CORE FRAMEWORK

### INTENT
**"We want to generate database/data-layer code for the specified data requirements mentioned in DATA declarations"**

### CREATE
**"Generate data implementation code based on requirements as per DATA declaration, architecture, technology stack, and storage format"**

### BUILD
**"Implement data layer code as per database design plan with high-quality code, precision, accuracy, and low error probability on execution"**

---

## PROCESS WORKFLOW

### STEP-1: Understand Data Requirements
```
ANALYZE:
  ✓ data_name and purpose
  ✓ connect type (database, api, session, cache, etc.)
  ✓ source location and endpoint
  ✓ schema structure (fields, types)
  ✓ create definition (structure, relationships)
  ✓ access control (public/private/authenticated)
  ✓ storage needs (persistent, temporary, session)
  ✓ checkpoint validation rules
  ✓ signal events and triggers
  ✓ SEARCH capabilities needed
```

### STEP-2: Choose Technology Stack
```
IF tech_stack NOT explicitly mentioned:
    DECIDE best tech stack based on:
    ✓ connect type requirements
    ✓ data volume and scale
    ✓ performance needs
    ✓ security requirements
    ✓ existing infrastructure
    STORE tech_stack in LOCAL_MEMORY.CACHE()
ELSE:
    RETRIEVE user-defined tech_stack
    STORE in LOCAL_MEMORY.CACHE()

TECH_STACK_OPTIONS by connect type:
  database (SQL):
    - PostgreSQL + Node.js/Python
    - MySQL + Node.js/Python
    - MongoDB + Node.js/Python
    
  database (NoSQL):
    - MongoDB + Node.js/Python/Go
    - Firebase + JavaScript/Python
    - DynamoDB + Node.js/Python
    
  api:
    - REST API + Node.js/Python/Go
    - GraphQL + Node.js/TypeScript
    - gRPC + Go/Python/Java
    
  cache:
    - Redis + Node.js/Python/Go
    - Memcached + Node.js/Python/Java
    - In-memory + any language
    
  session:
    - Express-session + Node.js
    - Flask-session + Python
    - Cookie-based + any language
    
  stream:
    - Kafka + Python/Go/Node.js
    - RabbitMQ + Python/Node.js/Go
    - AWS Kinesis + Python/Go/Node.js
```

### STEP-3: Retrieve Tech Stack and Apply Rules
```
RETRIEVE: tech_stack from LOCAL_MEMORY.CACHE()
RETRIEVE: data declaration requirements

APPLY: Language-specific best practices:
  ✓ Naming conventions (snake_case, camelCase, PascalCase)
  ✓ Type definitions (static vs dynamic)
  ✓ Connection patterns
  ✓ Error handling
  ✓ Validation methods
  ✓ Security practices
  ✓ Performance optimization
  ✓ Async/await patterns
  ✓ Transaction handling
  ✓ Index creation

REVIEW: Standards and guidelines:
  ✓ OWASP security guidelines
  ✓ Database best practices
  ✓ Connection pooling
  ✓ Query optimization
  ✓ Caching strategies
```

### STEP-4: List Requirements and Create Checklist
```
FOR each data source:
    EXTRACT:
    □ Schema definition (fields, types, relationships)
    □ Primary keys and indexes
    □ Validation rules (checkpoint)
    □ Access control rules (public/private)
    □ Event triggers (signal)
    □ Search/query capabilities (SEARCH)
    □ Caching strategy
    □ Retention policy
    □ Transformation rules (alter)
    □ Error handling
    □ Encryption needs
    □ Audit logging

CREATE: Implementation checklist
    □ Database schema creation
    □ Connection establishment
    □ Model/entity definition
    □ Query builders
    □ Validation middleware
    □ Error handlers
    □ Event emitters
    □ Cache layer
    □ Migration scripts
    □ Seed data (if needed)
```

### STEP-5: Plan Code Generation Route Map
```
PLAN the whole data layer like a route map:

EXAMPLE:
  "Database connection → Schema definition → 
   Model creation → Validation rules → 
   Query builders → Event handlers → 
   Cache layer → Error handling → 
   Audit logging"

SIMILAR: Plan data code generation with:
  ✓ Understanding of data requirements (checklist)
  ✓ Understanding of tech stack (language rules)
  ✓ Connection setup strategy
  ✓ Schema migration path
  ✓ Model/entity generation path
  ✓ Validation implementation path
  ✓ Query optimization path
  ✓ Caching strategy path
  ✓ Security implementation path
```

### STEP-6: Execute Plan and Generate Code
```
EXECUTE the planned route:
  1. Generate connection configuration
  2. Create schema/model definitions
  3. Implement validation layer
  4. Build query interfaces
  5. Add event handlers
  6. Implement caching
  7. Add error handling
  8. Create migration files
  9. Setup audit logging
  10. Generate helper utilities
```

---

## ALTER: Modification and Changes

```
WHEN user requests modifications:
  
  STEP-1: OBTAIN CLARITY
    ✓ Ask: "What specific field or data source needs modification?"
    ✓ Ask: "Should this change affect other connected data?"
    ✓ Ask: "Do you need backward compatibility?"
    ✓ Ask: "Any performance or security implications?"
    
  STEP-2: SPECIFY CHANGES
    ✓ Allow user to detail specific modifications
    ✓ Ask clarifying questions if needed
    ✓ Document change requirements
    ✓ Identify impact on other systems
    
  STEP-3: APPLY CHANGES
    ✓ Create migration script
    ✓ Update schema definition
    ✓ Update model/validation
    ✓ Update tests
    ✓ Update documentation
    
  NOTE: Only ask questions with user permission
```

---

## PROTECT: Security and Validation

```
SECURITY CHECKS:

  □ Review all data types for security
  □ Check for SQL injection vulnerabilities
  □ Verify encryption usage for sensitive fields
  □ Validate input sanitization
  □ Check connection security (TLS/SSL)
  □ Verify access control implementation
  □ Check for password hashing (if applicable)
  □ Validate authentication mechanisms
  □ Review audit logging setup
  □ Check for exposed credentials
  
PACKAGE VALIDATION:

  □ Check for vulnerable packages
  □ Verify package versions are current
  □ Review package security advisories
  □ Ensure no deprecated packages used
  □ Validate license compliance
  □ Check for supply chain risks
  □ Verify package integrity
  
RULE: Each line of code must be examined for:
  ✓ Security vulnerabilities
  ✓ Performance issues
  ✓ Data integrity concerns
  ✓ Error handling completeness
  ✓ Compliance with standards
  ✓ Best practices alignment
```

---

## MAINTAIN: Version Control and History

```
VERSIONING:

  NAME each generated version:
    data_layer_v1.0.0
    data_layer_v1.1.0 (with modifications)
    data_layer_v2.0.0 (major changes)
    
  STORE every version in LOG:
    {
      version: "1.0.0",
      timestamp: "2025-12-31T18:00:00Z",
      changes: "Initial data layer implementation",
      affected_entities: ["donors", "requests"],
      rollback_available: true
    }
    
  ENABLE VERSION MANAGEMENT:
    ✓ View specific version
    ✓ Compare versions
    ✓ Rollback to previous version
    ✓ Track all changes
    ✓ Document modifications
```

---

## MANAGE: Version and Change Management

```
MANAGE all code versions:

  TRACK changes explicitly:
    ✓ What changed
    ✓ Why it changed
    ✓ When it changed
    ✓ Who requested the change
    
  ALLOW user to:
    ✓ View version history
    ✓ Access specific versions
    ✓ Compare versions
    ✓ Understand changes
    ✓ Request rollback if needed
    
  MAINTAIN change log:
    Version 1.0.0: Initial implementation
    Version 1.1.0: Added encryption for phone field
    Version 1.2.0: Implemented indexing on email
    Version 2.0.0: Migrated from SQL to NoSQL
```

---

## COLLABORATE: Use Available Resources

```
COLLABORATE with available systems:

  □ Use database best practice tools
  □ Leverage validation libraries
  □ Use security scanning tools
  □ Employ testing frameworks
  □ Use documentation generators
  □ Leverage ORM/query builders
  □ Use schema migration tools
  □ Employ performance profilers
  
  GOAL: Produce high-quality code with:
    ✓ Low execution errors
    ✓ High security standards
    ✓ Optimal performance
    ✓ Complete test coverage
    ✓ Excellent documentation
```

---

## EXECUTE: Comprehensive Code Generation

```
CONSIDER all objectives:
  1. ✓ Data requirements understood
  2. ✓ Tech stack chosen and cached
  3. ✓ Rules and standards applied
  4. ✓ Requirements checklist created
  5. ✓ Route map planned
  6. ✓ Modifications handled
  7. ✓ Security validated
  8. ✓ Version managed
  9. ✓ Collaborative tools used
  10. ✓ All monitoring in place

EXECUTE all actions with above objectives in mind
REFERENCE LOCAL_MEMORY.CACHE() for context
GENERATE complete, production-ready data layer code
```

---

## MONITOR: Boundaries and Limits

```
MONITOR all activities:

  CREATE boundaries:
    □ Specify token limits for code generation
    □ Set quality thresholds
    □ Define performance baselines
    □ Set security requirements
    
  MONITOR within boundaries:
    □ Code complexity (lines, cyclomatic)
    □ Query performance
    □ Memory usage
    □ Security compliance
    □ Error rates
    □ Test coverage
    
  TRACK metrics:
    □ Schema complexity
    □ Query optimization
    □ Cache effectiveness
    □ Error handling completeness
    □ Documentation coverage
    □ Security scan results
```

---

## TECHNOLOGY STACK SPECIFIC GUIDELINES

### Node.js + PostgreSQL

```javascript
RULES:
  □ Use async/await for all database operations
  □ Use connection pooling (pg module)
  □ Implement parameterized queries
  □ Use TypeScript for type safety
  □ Implement proper error handling
  □ Use ORMs like Prisma or Sequelize
  □ Implement input validation
  □ Use environment variables for secrets

EXAMPLE STRUCTURE:
  ├── db/
  │   ├── connection.js
  │   ├── migrations/
  │   └── seeds/
  ├── models/
  │   ├── User.js
  │   └── Donor.js
  ├── validation/
  │   ├── schemas.js
  │   └── validators.js
  ├── queries/
  │   ├── userQueries.js
  │   └── donorQueries.js
  └── config/
      └── database.js
```

### Python + MongoDB

```python
RULES:
  □ Use async drivers (motor) for async operations
  □ Implement connection pooling
  □ Use PyMongo or Pymongo async
  □ Type hints for all functions
  □ Use Pydantic for validation
  □ Implement proper error handling
  □ Use environment variables
  □ Structure with dataclasses

EXAMPLE STRUCTURE:
  ├── db/
  │   ├── connection.py
  │   └── client.py
  ├── models/
  │   ├── user.py
  │   └── donor.py
  ├── validation/
  │   ├── schemas.py
  │   └── validators.py
  ├── queries/
  │   ├── user_queries.py
  │   └── donor_queries.py
  └── config/
      └── database.py
```

### Go + PostgreSQL

```go
RULES:
  □ Use prepared statements
  □ Implement connection pooling
  □ Use database/sql package
  □ Use sqlc for type safety
  □ Implement context for timeouts
  □ Proper error handling
  □ Use struct tags for validation
  □ Implement middleware patterns

EXAMPLE STRUCTURE:
  ├── database/
  │   ├── connection.go
  │   ├── queries.sql
  │   └── models.go
  ├── repository/
  │   ├── user.go
  │   └── donor.go
  ├── validation/
  │   └── validator.go
  └── config/
      └── database.go
```

---

## CODE GENERATION EXAMPLES

### Example 1: Blood Donor Data Layer (Node.js + PostgreSQL)

```javascript
// Schema Definition
CREATE TABLE donors (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL UNIQUE,
  phone VARCHAR(20) ENCRYPTED,
  blood_type VARCHAR(3) NOT NULL CHECK (blood_type IN ('A', 'B', 'AB', 'O')),
  verified BOOLEAN DEFAULT false,
  last_donation TIMESTAMP,
  location POINT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_donors_blood_type ON donors(blood_type);
CREATE INDEX idx_donors_location ON donors USING GIST(location);
CREATE INDEX idx_donors_verified ON donors(verified) WHERE verified = true;

// Connection Module
const { Pool } = require('pg');
const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
  max: 20,
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000,
});

// Model Definition
class Donor {
  static async create(donorData) {
    const { name, email, phone, blood_type } = donorData;
    const query = `
      INSERT INTO donors (name, email, phone, blood_type, verified)
      VALUES ($1, $2, $3, $4, $5)
      RETURNING *
    `;
    try {
      const result = await pool.query(query, [name, email, phone, blood_type, false]);
      return result.rows[0];
    } catch (error) {
      throw new Error(`Failed to create donor: ${error.message}`);
    }
  }
  
  static async findByBloodType(blood_type) {
    const query = `
      SELECT * FROM donors 
      WHERE blood_type = $1 AND verified = true
      ORDER BY distance ASC
    `;
    try {
      const result = await pool.query(query, [blood_type]);
      return result.rows;
    } catch (error) {
      throw new Error(`Failed to fetch donors: ${error.message}`);
    }
  }
}

module.exports = Donor;
```

### Example 2: User Preferences Data Layer (Python + MongoDB)

```python
from pymongo import MongoClient
from pydantic import BaseModel, EmailStr
from typing import Optional
from datetime import datetime

class UserPreferences(BaseModel):
    user_id: str
    source_location: str
    destination: str
    start_date: datetime
    end_date: datetime
    budget_min: float
    budget_max: float
    preferences: dict
    created_at: datetime = datetime.now()

class UserPreferencesRepository:
    def __init__(self, mongo_uri: str):
        self.client = MongoClient(mongo_uri)
        self.db = self.client['travel_app']
        self.collection = self.db['user_preferences']
        self._create_indexes()
    
    def _create_indexes(self):
        """Create necessary indexes"""
        self.collection.create_index('user_id')
        self.collection.create_index('created_at')
    
    async def create(self, preferences: UserPreferences):
        """Create new user preferences"""
        try:
            result = await self.collection.insert_one(preferences.dict())
            return str(result.inserted_id)
        except Exception as e:
            raise ValueError(f"Failed to create preferences: {str(e)}")
    
    async def find_by_user(self, user_id: str):
        """Find preferences by user ID"""
        try:
            return await self.collection.find_one({'user_id': user_id})
        except Exception as e:
            raise ValueError(f"Failed to fetch preferences: {str(e)}")
```

---

## BEST PRACTICES

### 1. Schema Design
```
✅ Use appropriate data types
✅ Define primary and foreign keys
✅ Create indexes for frequently queried fields
✅ Normalize data structure
✅ Document relationships

❌ Over-normalize (performance)
❌ Skip indexes for common queries
❌ Unclear field naming
❌ Missing constraints
```

### 2. Connection Management
```
✅ Use connection pooling
✅ Set connection timeouts
✅ Handle connection errors
✅ Close connections properly
✅ Monitor connection usage

❌ Create new connections per query
❌ No timeout handling
❌ Silent connection failures
❌ Connection leaks
```

### 3. Query Optimization
```
✅ Use prepared statements
✅ Implement pagination
✅ Use appropriate indexes
✅ Limit result sets
✅ Cache frequently accessed data

❌ String concatenation for queries
❌ No pagination
❌ Missing indexes
❌ Fetch all data
```

### 4. Error Handling
```
✅ Specific error types
✅ Meaningful error messages
✅ Retry logic for transient errors
✅ Logging of errors
✅ Graceful degradation

❌ Generic errors
❌ Silent failures
❌ No retry logic
❌ No error logging
```

### 5. Security
```
✅ Parameterized queries
✅ Input validation
✅ Encryption for sensitive data
✅ Access control
✅ Audit logging

❌ SQL injection vulnerable
❌ No validation
❌ Unencrypted sensitive data
❌ No access control
❌ No audit trail
```

---

## QUICK CHECKLIST

### Before Generating Code
- [ ] Data requirements fully understood
- [ ] Technology stack chosen
- [ ] Schema design planned
- [ ] Access control requirements identified
- [ ] Security requirements documented
- [ ] Performance expectations set
- [ ] Backup strategy defined
- [ ] Monitoring plan created

### While Generating Code
- [ ] Connection management implemented
- [ ] Schema creation included
- [ ] Model/Entity classes created
- [ ] Validation layer implemented
- [ ] Query builders created
- [ ] Error handling added
- [ ] Logging implemented
- [ ] Tests prepared

### After Generating Code
- [ ] Security review completed
- [ ] Performance testing done
- [ ] Test coverage verified
- [ ] Documentation created
- [ ] Migration scripts included
- [ ] Rollback plan prepared
- [ ] Version tracked
- [ ] Ready for production

---

