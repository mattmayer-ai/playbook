# Part 3: Infrastructure Setup

**Purpose**: Rapidly configure projects for scalable development using the context from knowledge handoff.

**Principle**: Standardize what you can. Deviate deliberately, not accidentally.

***

## Why Infrastructure Setup Comes After Discovery

You have:

* Validated problem statement
* User research insights
* Technical constraints documented
* PRD structured for Cursor

Now translate requirements into working infrastructure. This isn't "make it perfect"—it's "make it right for this specific product."

***

## Decision Frameworks (Not Prescriptions)

Every project is different. These frameworks help you choose the right stack for your requirements.

### Framework 1: Platform Choice

**Question**: Web, mobile, or both?

**Decision tree**:

```
Is primary use case on-the-go (location-based, camera, push notifications)?
├─ Yes → Mobile-first
│  └─ React Native (cross-platform) or Native (if performance-critical)
└─ No → Web-first
   └─ Next.js (if SEO matters) or Vite + React (if SPA is fine)
```

**From your constraints**:

* Check `CONSTRAINTS.md` → Platform section
* Check `PRD.md` → User flows (do they need native capabilities?)

**Example (TakeCost)**:

* Primary user: Contractors in office
* Need: Upload PDFs, review estimates
* Decision: Web-first (Next.js for SEO)
* Defer: Mobile app until validated web demand

### Framework 2: Backend Choice

**Question**: BaaS or custom backend?

**Decision tree**:

```
Do you need rapid MVP with auth + database + files?
├─ Yes → Consider BaaS
│  ├─ Open-source preference? → Supabase
│  └─ Speed over flexibility? → Firebase
└─ No → Custom backend
   ├─ Complex business logic? → Node.js + Express (or Fastify)
   ├─ Need strong typing? → Node.js + TypeScript + tRPC
   └─ Performance critical? → Go or Rust
```

**From your constraints**:

* Check `CONSTRAINTS.md` → Infrastructure section (any restrictions?)
* Check `PRD.md` → Complexity of business logic
* Check `PRD.md` → Timeline (MVP in 4 weeks? → BaaS)

**Example (CNS Platform)**:

* Complex: Multi-agent orchestration, experiment management
* Timeline: 8 weeks for MVP
* Decision: Custom backend (Node + TypeScript + AWS Bedrock)
* BaaS wouldn't handle multi-agent complexity

### Framework 3: Database Choice

**Question**: What database fits the data model?

**Decision tree**:

```
What's your data structure?
├─ Nested documents, flexible schema → Document DB (MongoDB, Firestore)
├─ Relational data, strong consistency → PostgreSQL
├─ Graph relationships → Neo4j or PostgreSQL + custom queries
└─ Time-series data → InfluxDB or TimescaleDB
```

**From your constraints**:

* Check `PRD.md` → Data Model section
* Check `CONSTRAINTS.md` → Data residency requirements
* Check `PRD.md` → Query patterns (read-heavy? write-heavy?)

**Example (Air Canada iPad Training)**:

* Data: Users, courses, progress (relational)
* Requirement: Offline-first, sync when online
* Decision: SQLite (local) + PostgreSQL (server)
* Why: SQLite handles offline, PostgreSQL for server sync

### Framework 4: State Management

**Question**: How to handle data fetching and global state?

**Decision tree**:

```
Server state (API data):
└─ React Query or SWR (automatic caching, refetching, loading states)

Client state (UI state):
├─ Simple (theme, modals) → Context API
├─ Medium complexity → Zustand
└─ Complex (time-travel debugging) → Redux Toolkit
```

**From your constraints**:

* Check `PRD.md` → How much data comes from API vs local?
* Check `PRD.md` → Complexity of UI state

**Example (EdPal)**:

* Server state: Lesson plans, user data (React Query)
* Client state: Current subject filter, sidebar open (Zustand)
* Why: Separate concerns, don't mix API cache with UI state

### Framework 5: Compliance Requirements

**Question**: What security/compliance patterns do we need?

**Decision tree**:

```
Is this a regulated industry?
├─ Healthcare → HIPAA patterns
│  ├─ No PHI in logs
│  ├─ Audit all data access
│  ├─ Encrypt at rest + transit
│  └─ Consent management
├─ Financial → PCI-DSS patterns
│  ├─ Never store payment data
│  ├─ Use tokenization (Stripe, etc.)
│  └─ TLS 1.2+ for transmission
└─ General → Privacy best practices
   ├─ Data minimization
   ├─ Explicit consent
   └─ Right to deletion
```

**From your constraints**:

* Check `CONSTRAINTS.md` → Compliance section
* Check `CONTEXT.md` → Industry context

**Example (Healthcare product)**:

```typescript
// Audit logging pattern
async function logDataAccess(
  userId: string,
  resourceType: string,
  resourceId: string,
  action: 'read' | 'write' | 'delete'
) {
  await auditLog.create({
    userId,
    resourceType,
    resourceId,
    action,
    timestamp: new Date(),
    ipAddress: getRequestIP() // Don't log if it contains PII
  });
}

// Use before any PHI access
await logDataAccess(user.id, 'MedicalRecord', recordId, 'read');
const record = await fetchMedicalRecord(recordId);
```

***

## Standard Setup Sequence

Once you've made stack decisions, follow this sequence. Same order every time.

### Step 1: Repository Initialization

```bash
# Initialize Git
git init
git branch -m main

# Create .gitignore
# [Use appropriate template for stack: Node, React Native, etc.]

# First commit (empty, just to establish main branch)
git add .gitignore
git commit -m "chore: initialize repository"
```

**What goes in .gitignore**:

* `node_modules/`
* `.env` (but not `env.template`)
* Build outputs (`dist/`, `build/`, `.next/`)
* IDE files (`.vscode/`, `.idea/`)
* OS files (`.DS_Store`)
* Stack-specific (e.g., React Native: `android/app/build/`, `ios/Pods/`)

### Step 2: TypeScript Configuration

```bash
# Install TypeScript
npm install -D typescript @types/node

# Create tsconfig.json
npx tsc --init
```

**Standard tsconfig.json**:

```json
{
  "compilerOptions": {
    // Strict mode (always)
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    
    // Module resolution
    "module": "ESNext",
    "moduleResolution": "bundler",
    "target": "ES2020",
    
    // Path aliases (reduces ../../../)
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"],
      "@components/*": ["src/components/*"],
      "@services/*": ["src/services/*"],
      "@utils/*": ["src/utils/*"],
      "@types/*": ["src/types/*"]
    },
    
    // Code generation
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist", "build"]
}
```

**Why strict mode**: Catches edge cases at compile time, not runtime. Retrofitting strict mode later is painful.

### Step 3: Code Quality Tools

```bash
# ESLint
npm install -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin

# Prettier
npm install -D prettier eslint-config-prettier

# If React
npm install -D eslint-plugin-react eslint-plugin-react-hooks
```

**.eslintrc.js**:

```javascript
module.exports = {
  parser: '@typescript-eslint/parser',
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react/recommended', // if React
    'plugin:react-hooks/recommended', // if React
    'prettier' // Must be last
  ],
  rules: {
    '@typescript-eslint/no-explicit-any': 'error',
    '@typescript-eslint/explicit-function-return-type': 'warn',
    'no-console': ['warn', { allow: ['warn', 'error'] }]
  },
  settings: {
    react: {
      version: 'detect'
    }
  }
};
```

**.prettierrc.js**:

```javascript
module.exports = {
  semi: true,
  trailingComma: 'es5',
  singleQuote: true,
  printWidth: 100,
  tabWidth: 2
};
```

### Step 4: Folder Structure

**Standard structure** (adjust for web vs mobile):

```
project-root/
├── src/
│   ├── components/         # Reusable UI components
│   │   ├── common/         # Buttons, inputs, modals
│   │   └── features/       # Feature-specific components
│   ├── screens/            # Full screens (mobile) or pages/ (web)
│   ├── hooks/              # Custom React hooks
│   ├── services/           # API clients, business logic
│   │   ├── api/            # HTTP client, endpoints
│   │   └── [domain]/       # Domain-specific services
│   ├── utils/              # Pure functions, helpers
│   ├── types/              # Shared TypeScript types
│   ├── constants/          # Config values, enums
│   ├── config/             # App configuration
│   └── App.tsx             # Entry point
├── tests/                  # Test files (mirror src/ structure)
├── docs/                   # PRD, context, architecture
├── .cursorrules
├── .gitignore
├── .eslintrc.js
├── .prettierrc.js
├── tsconfig.json
├── package.json
└── README.md
```

**When to deviate**:

* **Feature-based structure**: When single feature dominates codebase, group by feature instead
* **Monorepo**: When sharing code across multiple apps, use packages/

**Example feature-based structure**:

```
src/
├── features/
│   ├── auth/
│   │   ├── components/
│   │   ├── hooks/
│   │   ├── services/
│   │   └── types/
│   └── experiments/
│       ├── components/
│       ├── hooks/
│       └── services/
└── shared/
    ├── components/
    └── utils/
```

### Step 5: Environment Variables

Create `env.template` (committed) and `.env` (gitignored).

**env.template**:

```bash
# API Configuration
API_BASE_URL=https://api.example.com
API_KEY=your_api_key_here

# Firebase (if applicable)
FIREBASE_API_KEY=your_firebase_api_key
FIREBASE_PROJECT_ID=your_project_id

# AWS (if applicable)
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key

# Feature Flags
FEATURE_AI_ENABLED=true
FEATURE_BETA_ACCESS=false

# Development
NODE_ENV=development
PORT=3000
```

**Document in README**:

```markdown
## Environment Setup

1. Copy `env.template` to `.env`
2. Fill in values (see team wiki for credentials)
3. Never commit `.env` to version control
```

### Step 6: Package Scripts

**Standard scripts** in `package.json`:

```json
{
  "scripts": {
    "dev": "vite", // or "next dev" or "react-native start"
    "build": "tsc && vite build",
    "start": "vite preview",
    "test": "jest",
    "test:watch": "jest --watch",
    "lint": "eslint src/",
    "lint:fix": "eslint src/ --fix",
    "format": "prettier --write src/",
    "type-check": "tsc --noEmit"
  }
}
```

**Pre-commit hook** (optional but recommended):

```bash
npm install -D husky lint-staged

# package.json
{
  "lint-staged": {
    "*.{ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  }
}
```

### Step 7: Testing Setup

```bash
# Jest
npm install -D jest @types/jest ts-jest

# React testing
npm install -D @testing-library/react @testing-library/jest-dom
```

**jest.config.js**:

```javascript
module.exports = {
  preset: 'ts-jest',
  testEnvironment: 'jsdom', // or 'node' for backend
  roots: ['<rootDir>/src', '<rootDir>/tests'],
  testMatch: ['**/*.test.ts', '**/*.test.tsx'],
  moduleNameMapper: {
    // Match tsconfig paths
    '^@/(.*)$': '<rootDir>/src/$1',
    '^@components/(.*)$': '<rootDir>/src/components/$1',
    '^@services/(.*)$': '<rootDir>/src/services/$1'
  },
  setupFilesAfterEnv: ['<rootDir>/jest.setup.js']
};
```

**jest.setup.js**:

```javascript
// Mock environment variables
process.env = {
  ...process.env,
  API_BASE_URL: 'http://localhost:3000/api',
  NODE_ENV: 'test'
};

// Mock external services (example: Firebase)
jest.mock('firebase/app', () => ({
  initializeApp: jest.fn()
}));

// Mock fetch if needed
global.fetch = jest.fn();
```

***

## Compliance Patterns

These are implementation patterns for common compliance requirements. Add to your codebase as needed.

### HIPAA: No PHI in Logs

```typescript
// services/logger.ts
type LogLevel = 'info' | 'warn' | 'error';

interface LogContext {
  [key: string]: any;
}

function sanitizeContext(context: LogContext): LogContext {
  const sanitized = { ...context };
  
  // Remove any keys that might contain PHI
  const phiKeys = ['name', 'email', 'phone', 'ssn', 'dob', 'medical_record_number'];
  
  phiKeys.forEach(key => {
    if (key in sanitized) {
      sanitized[key] = '[REDACTED]';
    }
  });
  
  return sanitized;
}

export function log(level: LogLevel, message: string, context?: LogContext) {
  const sanitizedContext = context ? sanitizeContext(context) : {};
  
  console[level](message, sanitizedContext);
  
  // Send to logging service (e.g., CloudWatch, Datadog)
  // logService.send(level, message, sanitizedContext);
}

// Usage
log('info', 'User logged in', { userId: user.id, name: user.name });
// Logs: "User logged in" { userId: "123", name: "[REDACTED]" }
```

### HIPAA: Audit Trails

```typescript
// services/audit.ts
enum AuditAction {
  CREATE = 'create',
  READ = 'read',
  UPDATE = 'update',
  DELETE = 'delete'
}

interface AuditEntry {
  userId: string;
  action: AuditAction;
  resourceType: string;
  resourceId: string;
  timestamp: Date;
  ipAddress?: string;
  changes?: Record<string, any>; // What changed (for UPDATE)
}

async function createAuditEntry(entry: AuditEntry): Promise<void> {
  // Store in append-only audit log (never delete)
  await db.auditLog.create(entry);
}

// Middleware for API routes (example with Express)
export function auditMiddleware(
  resourceType: string,
  action: AuditAction
) {
  return async (req: Request, res: Response, next: NextFunction) => {
    const userId = req.user?.id;
    const resourceId = req.params.id;
    
    if (!userId) {
      return res.status(401).json({ error: 'Unauthorized' });
    }
    
    await createAuditEntry({
      userId,
      action,
      resourceType,
      resourceId,
      timestamp: new Date(),
      ipAddress: req.ip
    });
    
    next();
  };
}

// Usage in routes
app.get(
  '/api/medical-records/:id',
  auditMiddleware('MedicalRecord', AuditAction.READ),
  async (req, res) => {
    const record = await getMedicalRecord(req.params.id);
    res.json(record);
  }
);
```

### HIPAA: Consent Management

```typescript
// types/consent.ts
enum ConsentType {
  DATA_COLLECTION = 'data_collection',
  DATA_SHARING = 'data_sharing',
  MARKETING = 'marketing',
  RESEARCH = 'research'
}

enum ConsentStatus {
  GRANTED = 'granted',
  DENIED = 'denied',
  PENDING = 'pending',
  REVOKED = 'revoked'
}

interface Consent {
  id: string;
  userId: string;
  type: ConsentType;
  status: ConsentStatus;
  grantedAt?: Date;
  revokedAt?: Date;
  expiresAt?: Date;
}

// services/consent.ts
async function checkConsent(
  userId: string,
  consentType: ConsentType
): Promise<boolean> {
  const consent = await db.consent.findFirst({
    where: { userId, type: consentType }
  });
  
  if (!consent) return false;
  if (consent.status !== ConsentStatus.GRANTED) return false;
  if (consent.expiresAt && consent.expiresAt < new Date()) return false;
  
  return true;
}

async function grantConsent(
  userId: string,
  consentType: ConsentType,
  expiresInDays?: number
): Promise<Consent> {
  const expiresAt = expiresInDays
    ? new Date(Date.now() + expiresInDays * 24 * 60 * 60 * 1000)
    : undefined;
  
  return await db.consent.create({
    userId,
    type: consentType,
    status: ConsentStatus.GRANTED,
    grantedAt: new Date(),
    expiresAt
  });
}

// Usage before collecting data
if (!await checkConsent(userId, ConsentType.DATA_COLLECTION)) {
  throw new Error('User has not granted data collection consent');
}

// Collect data...
```

### Firebase: Security Rules (Start Closed)

**firestore.rules** (start restrictive, open deliberately):

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Default: deny everything
    match /{document=**} {
      allow read, write: if false;
    }
    
    // Open specific paths
    match /users/{userId} {
      // Users can only read/write their own data
      allow read, write: if request.auth != null 
        && request.auth.uid == userId;
    }
    
    match /experiments/{experimentId} {
      // Experiments are readable by authenticated users
      allow read: if request.auth != null;
      
      // Only owners can write
      allow write: if request.auth != null
        && request.auth.uid == resource.data.ownerId;
    }
  }
}
```

**storage.rules**:

```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    // Default: deny everything
    match /{allPaths=**} {
      allow read, write: if false;
    }
    
    // User uploads (images, documents)
    match /users/{userId}/{allPaths=**} {
      allow read: if request.auth != null 
        && request.auth.uid == userId;
      
      allow write: if request.auth != null
        && request.auth.uid == userId
        && request.resource.size < 10 * 1024 * 1024; // Max 10MB
    }
  }
}
```

***

## Documentation Templates

### README.md Structure

````markdown
# [Product Name]

[One-line description from PRD]

## Overview

[Brief summary: what this product does, who it's for, what problem it solves]

## Tech Stack

- **Frontend**: [Technology]
- **Backend**: [Technology or BaaS]
- **Database**: [Technology]
- **Hosting**: [Platform]
- **Key Services**: [External integrations]

## Prerequisites

- Node.js 18+
- [Other requirements: Firebase account, AWS credentials, etc.]

## Getting Started

1. Clone the repository
   ```bash
   git clone [repo-url]
   cd [project-name]
````

2.  Install dependencies

    ```bash
    npm install
    ```
3.  Set up environment variables

    ```bash
    cp env.template .env
    # Edit .env with your values (see team wiki for credentials)
    ```
4.  Run development server

    ```bash
    npm run dev
    ```
5.  Run tests

    ```bash
    npm test
    ```

## Project Structure

```
src/
├── components/   # Reusable UI components
├── screens/      # Full screens (or pages/)
├── services/     # API clients, business logic
├── hooks/        # Custom React hooks
├── utils/        # Pure functions
└── types/        # TypeScript types
```

## Key Documentation

* [PRD](../docs/PRD.md) - Product requirements and scope
* [Architecture](../docs/ARCHITECTURE.md) - Technical decisions
* [Constraints](../docs/CONSTRAINTS.md) - Technical and compliance requirements
* [Context](../docs/CONTEXT.md) - Domain knowledge

## Development Workflow

1. Create feature branch: `git checkout -b feat/feature-name`
2. Write code following `.cursorrules`
3. Run linter: `npm run lint`
4. Run tests: `npm test`
5. Commit with conventional format: `feat(scope): description`
6. Push and create PR

## Deployment

\[Instructions for deploying to staging and production]

## Contributing

See [.cursorrules](../.cursorrules/) for coding standards and patterns.

## License

\[License type]

```

---

## Summary: Infrastructure Setup

**Decision frameworks** (not prescriptions):
1. Platform: Web vs mobile vs both
2. Backend: BaaS vs custom
3. Database: Document vs relational vs specialized
4. State: Server state (React Query) vs client state (Zustand/Context)
5. Compliance: Healthcare, financial, or general privacy

**Standard setup sequence**:
1. Git + .gitignore
2. TypeScript (strict mode)
3. ESLint + Prettier
4. Folder structure
5. Environment variables
6. Package scripts
7. Testing setup

**Compliance patterns**:
- HIPAA: No PHI in logs, audit trails, consent management
- Firebase: Start closed, open deliberately

**Time investment**: 4-6 hours for complete setup

**Why it matters**: Standardized setup reduces cognitive overhead. When you return to a project after weeks, you know where things are and how they work.

---

**Next**: [Part 4: Iteration and Scaling](./Part_4_Iteration_and_Scaling.md)
```
