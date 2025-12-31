# MONGODB FORMAL SPECIFICATION 

## 12 PRIMARY MONGODB KEYWORDS

### 1. **DATABASE** - Database Selection & Management
```javascript
// Connect to database
db = client.database("myapp");

// List databases
db.adminCommand({ listDatabases: 1 });

// Drop database
db.dropDatabase();

// Rules: Use semantic database names, separate by environment
```

### 2. **COLLECTION** - Collection Operations
```javascript
// Create collection with schema validation
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "email"],
      properties: {
        _id: { bsonType: "objectId" },
        name: { bsonType: "string" },
        email: { bsonType: "string" }
      }
    }
  }
});

// Get collection
collection = db.collection("users");

// Drop collection
db.collection("users").drop();
```

### 3. **DOCUMENT** - CRUD Operations
```javascript
// Create (Insert)
db.users.insertOne({ name: "John", email: "john@example.com" });
db.users.insertMany([{ name: "Jane" }, { name: "Bob" }]);

// Read (Query)
db.users.findOne({ name: "John" });
db.users.find({ age: { $gt: 18 } });

// Update
db.users.updateOne({ _id: ObjectId("...") }, { $set: { age: 30 } });
db.users.updateMany({ status: "inactive" }, { $set: { active: false } });

// Delete
db.users.deleteOne({ _id: ObjectId("...") });
db.users.deleteMany({ status: "inactive" });
```

### 4. **SCHEMA** - Schema Design & Validation
```javascript
// Validation schema
{
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "email"],
      properties: {
        name: {
          bsonType: "string",
          minLength: 1,
          maxLength: 100
        },
        email: {
          bsonType: "string",
          pattern: "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$"
        },
        age: {
          bsonType: "int",
          minimum: 0,
          maximum: 150
        }
      }
    }
  }
}
```

### 5. **INDEX** - Indexing for Performance
```javascript
// Create indexes
db.users.createIndex({ email: 1 }, { unique: true });
db.users.createIndex({ name: 1, email: 1 }); // Compound
db.users.createIndex({ createdAt: -1 }); // Descending
db.users.createIndex({ location: "2dsphere" }); // Geospatial

// List indexes
db.users.getIndexes();

// Drop index
db.users.dropIndex("email_1");
```

### 6. **QUERY** - Advanced Query Operations
```javascript
// Filter operators
db.users.find({ age: { $gte: 18, $lte: 65 } }); // Range
db.users.find({ status: { $in: ["active", "pending"] } }); // In
db.users.find({ email: { $exists: true } }); // Exists

// Logical operators
db.users.find({
  $or: [
    { age: { $lt: 18 } },
    { age: { $gt: 65 } }
  ]
});

// Array operators
db.posts.find({ tags: { $all: ["mongodb", "database"] } });
db.posts.find({ tags: { $elemMatch: { $gt: 5 } } });
```

### 7. **AGGREGATION** - Data Aggregation Pipeline
```javascript
// Pipeline stages
db.users.aggregate([
  { $match: { status: "active" } },
  { $group: { _id: "$country", count: { $sum: 1 } } },
  { $sort: { count: -1 } },
  { $limit: 10 }
]);

// Complex aggregation
db.orders.aggregate([
  { $match: { createdAt: { $gte: ISODate("2024-01-01") } } },
  { $lookup: {
      from: "users",
      localField: "userId",
      foreignField: "_id",
      as: "user"
    }
  },
  { $unwind: "$user" },
  { $group: {
      _id: "$user.country",
      totalSales: { $sum: "$amount" }
    }
  }
]);
```

### 8. **TRANSACTION** - ACID Transactions
```javascript
// Start session
session = db.getMongo().startSession();

// Run transaction
session.startTransaction();
try {
  db.users.updateOne({ _id: user1Id }, { $inc: { balance: -100 } }, { session });
  db.users.updateOne({ _id: user2Id }, { $inc: { balance: 100 } }, { session });
  session.commitTransaction();
} catch (error) {
  session.abortTransaction();
  throw error;
} finally {
  session.endSession();
}
```

### 9. **REPLICATION** - Replica Sets
```javascript
// Connect to replica set
const client = new MongoClient(
  "mongodb://host1:27017,host2:27017,host3:27017",
  { replicaSet: "rs0" }
);

// Configure replica set
rs.initiate({
  _id: "rs0",
  members: [
    { _id: 0, host: "localhost:27017" },
    { _id: 1, host: "localhost:27018" },
    { _id: 2, host: "localhost:27019" }
  ]
});
```

### 10. **BACKUP** - Backup & Restore
```bash
# Backup database
mongodump --uri="mongodb://..." --out=/backup/path

# Restore database
mongorestore --uri="mongodb://..." /backup/path

# Backup specific collection
mongodump --uri="mongodb://..." --collection=users --out=/backup

# Restore specific collection
mongorestore --uri="mongodb://..." --collection=users /backup
```

### 11. **SECURITY** - Authentication & Authorization
```javascript
// Create user with role
db.createUser({
  user: "appuser",
  pwd: passwordPrompt(),
  roles: [
    { role: "readWrite", db: "myapp" }
  ]
});

// Enable authentication
mongod --auth

// Connect with authentication
const client = new MongoClient(
  "mongodb://appuser:password@localhost:27017/myapp"
);
```

### 12. **MONITORING** - Performance & Monitoring
```javascript
// Current operations
db.currentOp();

// Query statistics
db.users.explain("executionStats").find({ age: { $gt: 18 } });

// Slow query log
db.getProfilingLevel();
db.setProfilingLevel(1); // Log slow queries

// Database stats
db.stats();

// Collection stats
db.users.stats();
```

## 6-STEP MONGODB GENERATION WORKFLOW

### STEP-1: UNDERSTAND DATA MODEL
- What entities needed?
- Relationships?
- Query patterns?
- Volume/scale?
- Replication requirements?

### STEP-2: SCHEMA DESIGN
```
Local memory cache:
- Collections defined
- Document structure
- Validation rules
- Index strategy
- Sharding approach
```

### STEP-3: RETRIEVE MONGODB RULES
```
Rules:
- Denormalize for read performance
- Use schema validation
- Index before querying
- Transactions for consistency
- Replica sets for HA
```

### STEP-4: REQUIREMENTS CHECKLIST
```
☐ Collections created with validation
☐ Indexes defined
☐ Aggregation pipelines planned
☐ Replication configured
☐ Backup strategy
☐ Security configured
☐ Monitoring enabled
☐ Query performance tested
```

### STEP-5: GENERATION ROADMAP
```
PHASE 1: SETUP
├─ Database creation
├─ Collection definitions
└─ Schema validation

PHASE 2: INDEXING
├─ Primary indexes
├─ Compound indexes
└─ Geospatial indexes

PHASE 3: OPERATIONS
├─ CRUD operations
├─ Aggregation pipelines
└─ Transactions

PHASE 4: REPLICATION
├─ Replica set config
├─ Primary/Secondary setup
└─ Failover testing

PHASE 5: SECURITY
├─ User creation
├─ Role assignment
└─ Auth configuration

PHASE 6: MONITORING
├─ Profiling
├─ Performance metrics
├─ Backup automation
└─ Alerts
```

### STEP-6: EXECUTE GENERATION
```javascript
// Database initialization script
db.createCollection("users", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "email"],
      properties: {
        _id: { bsonType: "objectId" },
        name: { bsonType: "string" },
        email: { bsonType: "string" },
        createdAt: { bsonType: "date" }
      }
    }
  }
});

// Create indexes
db.users.createIndex({ email: 1 }, { unique: true });
db.users.createIndex({ createdAt: -1 });

// Aggregation pipeline for reports
db.users.aggregate([
  { $match: { status: "active" } },
  { $group: { _id: "$country", count: { $sum: 1 } } },
  { $sort: { count: -1 } }
]);
```

## BEST PRACTICES
1. Design for read access patterns
2. Index strategically
3. Use schema validation
4. Replicate for HA
5. Monitor performance
6. Backup regularly
7. Use transactions carefully
8. Denormalize thoughtfully
9. Shard when needed
10. Test disaster recovery

---
