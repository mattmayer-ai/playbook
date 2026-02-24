# Part 4: Infrastructure Setup

**Purpose:** Rapidly configure projects for scalable development using the context from knowledge handoff.

**Principle:** Standardize what you can. Deviate deliberately, not accidentally.

**Time:** 4-6 hours

***

### Why Infrastructure Setup Comes After Discovery

You have:

* Validated problem statement
* User research insights
* Technical constraints documented
* PRD structured for Cursor

Now translate requirements into working infrastructure. This isn't "make it perfect"—it's "make it right for this specific product."

***

### Decision Frameworks (Not Prescriptions)

Every project is different. These frameworks help you choose the right stack for your requirements.

#### Framework 1: Platform Choice

**Question:** Web, mobile, or both?

**Decision tree:**

```
Is primary use case on-the-go (location-based, camera, push notifications)?
├─ Yes → Mobile-first
│  └─ React Native (cross-platform) or Native (if performance-critical)
└─ No → Web-first
   └─ Next.js (if SEO matters) or Vite + React (if SPA is fine)
```

**From your constraints:**

* Check CONSTRAINTS.md → Platform section
* Check PRD.md → User flows (do they need native capabilities?)

***

#### Framework 2: Backend Choice

**Question:** BaaS or custom backend?

**Decision tree:**

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

**From your constraints:**

* Check CONSTRAINTS.md → Infrastructure section (any restrictions?)
* Check PRD.md → Complexity of business logic
* Check PRD.md → Timeline (MVP in 4 weeks? → BaaS)

***

#### Framework 3: Database Choice

**Question:** What database fits the data model?

**Decision tree:**

```
What's your data structure?
├─ Nested documents, flexible schema → Document DB (MongoDB, Firestore)
├─ Relational data, strong consistency → PostgreSQL
├─ Graph relationships → Neo4j or PostgreSQL + custom queries
└─ Time-series data → InfluxDB or TimescaleDB
```

**From your constraints:**

* Check PRD.md → Data Model section
* Check CONSTRAINTS.md → Data residency requirements
* Check PRD.md → Query patterns (read-heavy? write-heavy?)

***

#### Framework 4: State Management

**Question:** How to handle data fetching and global state?

**Decision tree:**

```
Server state (API data):
└─ React Query or SWR (automatic caching, refetching, loading states)

Client state (UI state):
├─ Simple (theme, modals) → Context API
├─ Medium complexity → Zustand
└─ Complex (time-travel debugging) → Redux Toolkit
```

**From your constraints:**

* Check PRD.md → How much data comes from API vs local?
* Check PRD.md → Complexity of UI state

***

#### Framework 5: Compliance Requirements

**Question:** What security/compliance patterns do we need?

**Decision tree:**

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

**From your constraints:**

* Check CONSTRAINTS.md → Compliance section
* Check CONTEXT.md → Industry context

***

### Standard Setup Sequence

Once you've made stack decisions, follow this sequence. Same order every time.

#### Step 1: Repository Initialization

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

**What goes in .gitignore:**

* `node_modules/`
* `.env` (but not `env.template`)
* Build outputs (`dist/`, `build/`, `.next/`)
* IDE files (`.vscode/`, `.idea/`)
* OS files (`.DS_Store`)
* Stack-specific (e.g., React Native: `android/app/build/`, `ios/Pods/`)

***

#### Step 2: TypeScript Configuration

```bash
# Install TypeScript
npm install -D typescript @types/node

# Create tsconfig.json
npx tsc --init
```

**Standard tsconfig.json:**

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

**Why strict mode:** Catches edge cases at compile time, not runtime. Retrofitting strict mode later is painful.

***

#### Step 3: Code Quality Tools

```bash
# ESLint
npm install -D eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin

# Prettier
npm install -D prettier eslint-config-prettier

# If React
npm install -D eslint-plugin-react eslint-plugin-react-hooks
```

**.eslintrc.js:**

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

**.prettierrc.js:**

```javascript
module.exports = {
  semi: true,
  trailingComma: 'es5',
  singleQuote: true,
  printWidth: 100,
  tabWidth: 2
};
```

***

#### Step 4: Folder Structure

**Standard structure (adjust for web vs mobile):**

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

**When to deviate:**

* **Feature-based structure:** When single feature dominates codebase, group by feature instead
* **Monorepo:** When sharing code across multiple apps, use `packages/`

***

#### Step 5: Environment Variables

Create `env.template` (committed) and `.env` (gitignored).

**env.template:**

```
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

***

#### Step 6: Package Scripts

**Standard scripts in package.json:**

```json
{
  "scripts": {
    "dev": "vite",
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

**Pre-commit hook (optional but recommended):**

```bash
npm install -D husky lint-staged
```

```json
// package.json
{
  "lint-staged": {
    "*.{ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  }
}
```

***

#### Step 7: Testing Setup

```bash
# Jest
npm install -D jest @types/jest ts-jest

# React testing
npm install -D @testing-library/react @testing-library/jest-dom
```

**jest.config.js:**

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

***

### Compliance Patterns

These are implementation patterns for common compliance requirements.

#### HIPAA: No PHI in Logs

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
}

// Usage
log('info', 'User logged in', { userId: user.id, name: user.name });
// Logs: "User logged in" { userId: "123", name: "[REDACTED]" }
```

#### HIPAA: Audit Trails

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
}

async function createAuditEntry(entry: AuditEntry): Promise<void> {
  // Store in append-only audit log (never delete)
  await db.auditLog.create(entry);
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

#### Firebase: Security Rules (Start Closed)

```
// firestore.rules
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Default: deny everything
    match /{document=**} {
      allow read, write: if false;
    }
    
    // Open specific paths
    match /users/{userId} {
      allow read, write: if request.auth != null 
        && request.auth.uid == userId;
    }
  }
}
```

***

### Summary: Infrastructure Setup

**Decision frameworks (not prescriptions):**

1. Platform: Web vs mobile vs both
2. Backend: BaaS vs custom
3. Database: Document vs relational vs specialized
4. State: Server state (React Query) vs client state (Zustand/Context)
5. Compliance: Healthcare, financial, or general privacy

**Standard setup sequence:**

1. Git + .gitignore
2. TypeScript (strict mode)
3. ESLint + Prettier
4. Folder structure
5. Environment variables
6. Package scripts
7. Testing setup

**Compliance patterns:**

* HIPAA: No PHI in logs, audit trails, consent management
* Firebase: Start closed, open deliberately

**Time investment:** 4-6 hours for complete setup

**Why it matters:** Standardized setup reduces cognitive overhead. When you return to a project after weeks, you know where things are and how they work.

***

**Next: Part 5: Iteration and Scaling** — Handle pivots, refactoring, and infrastructure evolution.
